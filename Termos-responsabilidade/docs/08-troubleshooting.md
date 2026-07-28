# Solução de problemas

## O termo não aparece

```powershell
Get-ScheduledTask -TaskName "Empresa-Termos-NoLogon"

Get-ScheduledTaskInfo -TaskName "Empresa-Termos-NoLogon" |
    Format-List LastRunTime,LastTaskResult
```

Verificar o cliente:

```powershell
Select-String `
  -Path "C:\ProgramData\Empresa\NotebookTerms\TermsClient.ps1" `
  -Pattern "ClientVersion"
```

Verificar o log:

```powershell
Get-Content `
  "C:\ProgramData\Empresa\NotebookTerms\Logs\$(Get-Date -Format yyyy-MM-dd).log" `
  -Tail 30
```

Possíveis causas:

- usuário já possui aceite;
- usuário está em uma exceção;
- cliente antigo instalado;
- tarefa ausente ou falhando;
- GPO não aplicada;
- DNS, certificado ou servidor indisponível.

## O site não é confiável

```powershell
Resolve-DnsName "<URL-TERMOS>"
Test-NetConnection "<URL-TERMOS>" -Port 443
```

Confirmar que:

- o DNS retorna o servidor correto;
- o certificado contém o nome utilizado;
- a autoridade raiz foi aplicada ao computador;
- data e hora do computador estão corretas.

## O cliente ainda exibe comportamento antigo

Comparar a origem central e o arquivo instalado:

```powershell
Select-String -Path "<ORIGEM-CENTRAL>\TermsClient.ps1" -Pattern "ClientVersion"
Select-String -Path "C:\ProgramData\Empresa\NotebookTerms\TermsClient.ps1" -Pattern "ClientVersion"
```

Atualizar manualmente somente para diagnóstico:

```powershell
Copy-Item `
  -LiteralPath "<ORIGEM-CENTRAL>\TermsClient.ps1" `
  -Destination "C:\ProgramData\Empresa\NotebookTerms\TermsClient.ps1" `
  -Force
```

Depois corrigir a distribuição central, sem depender de cópia manual.

## Diagnóstico da GPO

```powershell
gpupdate /force
gpresult /Scope Computer /R
gpresult /H "C:\Windows\Temp\GPO-Termos.html" /F
```

Verificar GPOs antigas que possam copiar arquivos ou criar tarefas com o mesmo nome.

## Verificação do servidor

```powershell
Get-ScheduledTask -TaskName "Empresa-NotebookTerms-Server"
Invoke-RestMethod "https://<URL-TERMOS>/health"
```

## Código de retorno comum

| Resultado | Interpretação |
|---|---|
| `0` | execução concluída |
| `1` | erro tratado ou modo aberto |
| `2` | falha em modo fechado ou sessão bloqueada |
| tarefa ausente | instalação/GPO não concluída |

