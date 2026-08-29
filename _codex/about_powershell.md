# list top 10 largest folder in a dir windows

Get-ChildItem -Directory | ForEach-Object {
    $size = (Get-ChildItem -LiteralPath $_.FullName -Recurse -File -ErrorAction SilentlyContinue |
        Measure-Object -Property Length -Sum).Sum

    [PSCustomObject]@{
        Folder = $_.Name
        'Size (GB)' = [Math]::Round($size / 1GB, 2)
    }
} | Sort-Object 'Size (GB)' -Descending | Select-Object -First 10


# top 10 file extensions by total disk space used in the current directory and all subdirectories

Get-ChildItem -File -Recurse -ErrorAction SilentlyContinue |
    Group-Object Extension |
    ForEach-Object {
        [PSCustomObject]@{
            Extension = if ($_.Name) { $_.Name } else { '[No extension]' }
            'Size (GB)' = [math]::Round(($_.Group | Measure-Object Length -Sum).Sum / 1GB, 2)
            Files = $_.Count
        }
    } |
    Sort-Object 'Size (GB)' -Descending |
    Select-Object -First 10 |
    Format-Table -AutoSize
