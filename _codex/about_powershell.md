 list top 10 largest folder in a dir windows

Get-ChildItem -Directory | ForEach-Object {
    $size = (Get-ChildItem -LiteralPath $_.FullName -Recurse -File -ErrorAction SilentlyContinue |
        Measure-Object -Property Length -Sum).Sum

    [PSCustomObject]@{
        Folder = $_.Name
        'Size (GB)' = [Math]::Round($size / 1GB, 2)
    }
} | Sort-Object 'Size (GB)' -Descending | Select-Object -First 10
