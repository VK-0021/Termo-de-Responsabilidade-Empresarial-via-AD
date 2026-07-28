# Gestão de Termos de Responsabilidade

> Documentação técnica interna para implantação, operação e evolução do aceite eletrônico de termos em equipamentos Windows.

![Status](https://img.shields.io/badge/status-produção-1f7a4d)
![Plataforma](https://img.shields.io/badge/plataforma-Windows%20%2B%20AD-74262c)
![Acesso](https://img.shields.io/badge/acesso-repositório%20privado-555)

## Objetivo

Centralizar o aceite do Termo de Responsabilidade por usuário e equipamento, sem depender de licenças Premium do Microsoft Entra ID.

O sistema identifica cada aceite pela combinação:

```text
versão do termo + SID do usuário + UUID do equipamento
```

Quando qualquer um desses elementos muda, um novo aceite é solicitado.

## O que está documentado

| Documento | Finalidade |
|---|---|
| [Visão geral](docs/01-visao-geral.md) | Escopo, comportamento e critérios de sucesso |
| [Arquitetura](docs/02-arquitetura.md) | Componentes, integrações e fluxo de dados |
| [Implantação](docs/03-implantacao.md) | Preparação do servidor, DNS, TLS e aplicação |
| [Distribuição por GPO](docs/04-gpo.md) | Piloto, filtros, validação e expansão |
| [Operação](docs/05-operacao.md) | Rotinas administrativas e publicação de termos |
| [Seguranca e privacidade](docs/06-seguranca-privacidade.md) | Controles, dados pessoais e prevenção de vazamentos |
| [Backup e recuperação](docs/07-backup-recuperacao.md) | Cópia, restauração e continuidade |
| [Solucao de problemas](docs/08-troubleshooting.md) | Diagnósticos e comandos de verificação |
| [Histórico técnico](docs/09-historico-tecnico.md) | Funcionalidades e decisões implantadas |

## Estado atual da solução

- Cliente Windows em tela cheia.
- Bloqueio dos monitores secundários enquanto houver aceite pendente.
- Leitura integral obrigatória antes da liberação da declaração.
- CPF validado e armazenado de forma criptografada.
- Evidência com data e hora do servidor, identificadores técnicos e SHA-256.
- PDF individual e exportação CSV.
- Painel administrativo com contas individuais.
- Autenticação TOTP compatível com Microsoft Authenticator.
- Distribuição centralizada por GPO.
- URL HTTPS interna sem exposição direta do serviço de aplicação.

## Regras de publicação

Este repositório deve permanecer **privado**. Nunca publicar:

- bancos `*.db`, `*.db-wal` ou `*.db-shm`;
- `config.json` de produção;
- chaves de API, segredos de sessão ou hashes de credenciais;
- certificados privados `*.pfx` e respectivas senhas;
- PDFs, CSVs, logs ou capturas contendo dados reais;
- CPF, SID, serial, UUID, hostname, IP interno ou nomes de colaboradores;
- links de convite ou códigos de recuperação do segundo fator.

Consulte [SECURITY.md](SECURITY.md) antes de qualquer commit.

## Convenções

Todos os exemplos usam placeholders:

```text
<DOMINIO>
<SERVIDOR-TERMOS>
<URL-TERMOS>
<COMPARTILHAMENTO-GPO>
<CHAVE-API>
```

Substitua-os somente em documentação operacional armazenada em local restrito. Não faça commit dos valores reais.

## Responsáveis

- Proprietário do processo: Tecnologia da Informação
- Validação do conteúdo do termo: Jurídico
- Classificação da informação: Uso Interno Confidencial
- Revisão mínima recomendada: trimestral e após qualquer mudança relevante

