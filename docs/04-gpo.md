# Distribuição por GPO

## Escopo

A implantação utiliza configuração de computador, pois o instalador precisa gravar em `ProgramData` e criar uma tarefa agendada local.

## Estrutura recomendada

```text
OU de homologação
└── OU piloto do aceite
    └── computadores de teste
```

Vincule a GPO primeiro à OU piloto. Não vincule ao domínio inteiro antes da homologação.

## Configurações

### Script de inicialização

```text
Configuração do Computador
→ Políticas
→ Configurações do Windows
→ Scripts
→ Inicialização
→ Scripts do PowerShell
```

Cadastre somente uma entrada para o instalador. Use placeholders:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass `
  -File "\\<COMPARTILHAMENTO-GPO>\Install-Client.ps1" `
  -ServerUrl "https://<URL-TERMOS>" `
  -ApiKey "<CHAVE-API>" `
  -FailMode open
```

> A chave real não deve aparecer neste repositório. Proteja a leitura do compartilhamento e limite a exposição conforme o modelo adotado.

### Políticas complementares

- Sempre aguardar a rede na inicialização e no logon.
- Executar scripts PowerShell primeiro.
- Distribuir o certificado raiz em Autoridades de Certificação Raiz Confiáveis.

## Segurança do filtro

- `Domain Computers`: leitura e aplicação.
- Administradores responsáveis: leitura e edição.
- Evitar `Negar Aplicar Política de Grupo`, salvo exceção documentada.

## Conflito com GPOs antigas

Antes da expansão:

1. identificar todas as GPOs antigas de termo;
2. verificar scripts de logon, startup e tarefas agendadas;
3. garantir que apenas uma GPO gerencie `Empresa-Termos-NoLogon`;
4. garantir que apenas uma origem copie o cliente e sua configuração;
5. desvincular as GPOs antigas da OU piloto;
6. não depender da ordem de precedência para scripts que sobrescrevem arquivos.

## Validação no cliente

```powershell
gpupdate /force
gpresult /Scope Computer /R

Get-ScheduledTask -TaskName "Empresa-Termos-NoLogon"

(Get-ScheduledTask -TaskName "Empresa-Termos-NoLogon").Actions |
    Format-List Execute,Arguments
```

Gerar relatório detalhado:

```powershell
gpresult /H "C:\Windows\Temp\GPO-Termos.html" /F
Start-Process "C:\Windows\Temp\GPO-Termos.html"
```

## Ondas de implantação

1. TI.
2. Grupo piloto de usuários comuns.
3. Matriz por departamento.
4. Demais unidades com conectividade estável.
5. Obras remotas após validação de DNS, TLS e VPN.

