# Invoke-WebRequestで取得したHTML同士を比較する
`Compare-Object`には文字列の配列（行の一覧）を渡す必要がある。  

```ps1
function Get-HtmlContent($url)
{
    Invoke-WebRequest $url `
    | Select-Object -ExpandProperty Content `
    | % { $_.Split([Environment]::NewLine, [StringSplitOptions]::RemoveEmptyEntries) }
}

$html1 = Get-HtmlContent "https://foo.example.com"
$html2 = Get-HtmlContent "https://bar.example.com"

if (Compare-Object $html1 $html2)
{
    # 差分あり
}
else
{
    # 差分なし
}
```