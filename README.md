![Alt text](screenshot.png?raw=true "screenshot")


If you would like to "see" the rendered version, you'll need to start an HTTP server in the same directory as this repo.

There are many available:

https://gist.github.com/willurd/5720255

On a windows system:

```
$Hso = New-Object Net.HttpListener
$Hso.Prefixes.Add("http://+:8000/")
$Hso.Start()
While ($Hso.IsListening) {
    $HC = $Hso.GetContext()
    $HRes = $HC.Response
    $HRes.Headers.Add("Content-Type","text/plain")
    $Buf = [Text.Encoding]::UTF8.GetBytes((GC (Join-Path $Pwd ($HC.Request).RawUrl)))
    $HRes.ContentLength64 = $Buf.Length
    $HRes.OutputStream.Write($Buf,0,$Buf.Length)
    $HRes.Close()
}
$Hso.Stop()
```
