# Segurança

## Dados tratados

- Nome e conta corporativa.
- SID do usuário.
- CPF informado.
- Departamento e cargo, quando disponíveis.
- Hostname, UUID, serial, fabricante, modelo e patrimônio.
- Endereço IP, versão do cliente, data e hora.
- Texto e versão do termo.
- Hash e protocolo da evidência.

## Controles implantados

- HTTPS obrigatório.
- CPF validado no cliente e no servidor.
- CPF criptografado em repouso.
- Exibição mascarada no painel e CSV.
- Hash SHA-256 do texto e da evidência.
- Senhas administrativas derivadas com PBKDF2.
- Segundo fator TOTP.
- Códigos de recuperação de uso único.
- Limite persistente de tentativas incorretas.
- Sessões administrativas temporárias.
- Auditoria de eventos relevantes.

## Princípio do menor privilégio

- O cliente precisa apenas consultar pendência e registrar aceite.
- O painel exige autenticação administrativa.
- PDFs e exportações não devem ser públicos.
- A pasta de dados deve ser restrita à conta do serviço e administradores.
- O compartilhamento da GPO deve permitir leitura às contas de computador e escrita somente à TI.

## LGPD

O tratamento deve possuir finalidade definida, base legal avaliada e prazo de retenção aprovado. A documentação operacional deve registrar:

- finalidade da coleta;
- responsáveis pelo tratamento;
- prazo de retenção;
- procedimento para correção e atendimento ao titular;
- controles contra acesso indevido;
- processo de descarte seguro.

## Autenticação em duas etapas

- Sincronizar o relógio do servidor com fonte confiável.
- Bloquear após três códigos inválidos no período configurado.
- Não registrar códigos TOTP em logs.
- Redefinição do TOTP deve invalidar sessões e códigos anteriores.
- Manter conta de emergência protegida e testada.

## Modelo de ameaça resumido

| Risco | Controle |
|---|---|
| Interceptação | HTTPS e certificado confiável |
| Alteração do termo | Hash do conteúdo e versionamento |
| Falsificação do aceite | SID, UUID, hora do servidor e hash |
| Vazamento de CPF | Criptografia e mascaramento |
| Comprometimento administrativo | Senha forte, TOTP e limite de tentativas |
| Publicação acidental | Repositório privado, `.gitignore` e revisão |
| Indisponibilidade | Backup, conta de emergência e modo de falha definido |

