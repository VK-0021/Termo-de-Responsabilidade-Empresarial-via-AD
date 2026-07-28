# Backup e recuperação

## Escopo do backup

Incluir, de forma protegida:

- banco SQLite;
- configuração e segredos necessários à descriptografia;
- certificados privados necessários ao serviço;
- código implantado e versão do cliente;
- documentação de DNS, GPO e tarefa agendada.

Não armazenar backups neste repositório.

## Backup consistente

A forma mais simples é parar brevemente a tarefa durante a cópia:

```powershell
Stop-ScheduledTask -TaskName "Empresa-NotebookTerms-Server"

try {
    Copy-Item "<DIRETORIO-DADOS>" "<DESTINO-PROTEGIDO>" -Recurse -Force
}
finally {
    Start-ScheduledTask -TaskName "Empresa-NotebookTerms-Server"
}
```

Validar em seguida:

```powershell
Invoke-RestMethod "https://<URL-TERMOS>/health"
```

## Retenção sugerida

- Diário: 30 dias.
- Semanal: 12 semanas.
- Mensal: conforme política corporativa.
- Antes de mudanças: cópia imutável identificada.

O prazo definitivo deve ser aprovado pela TI, Segurança e Jurídico.

## Teste de restauração

1. Preparar servidor isolado.
2. Restaurar aplicação e dados.
3. Impedir comunicação com clientes de produção.
4. Iniciar o serviço.
5. Validar versões, administradores e contagens.
6. Gerar um PDF de evidência autorizado.
7. Registrar duração e problemas encontrados.

## Recuperação de desastre

1. Declarar incidente.
2. Preservar o servidor afetado.
3. Provisionar host substituto.
4. Restaurar a última cópia válida.
5. Recriar DNS e certificado quando necessário.
6. Validar `/health`.
7. Testar com cliente piloto.
8. Liberar os clientes por ondas.
9. Registrar perda de dados estimada e causa.

