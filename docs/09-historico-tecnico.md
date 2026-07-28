# Histórico técnico

## Fundação

- Aceite individual por versão, SID e UUID.
- Inventário básico de equipamento.
- Servidor central com SQLite.
- Painel, busca e exportação CSV.
- Cliente WPF em tela cheia.
- Instalação por GPO.

## Experiência do usuário

- Identidade visual institucional.
- Identificação do colaborador e equipamento.
- CPF compacto com máscara e validação.
- Seções numeradas.
- Barra de leitura acumulada.
- Declaração bloqueada até o final real do conteúdo.
- Orientação a cada tentativa antecipada.
- Fechamento silencioso após o aceite.
- Bloqueio dos monitores secundários.

## Evidência

- Patrimônio derivado do padrão de hostname.
- Tratamento específico para equipamentos locados.
- Protocolo único.
- PDF individual multipágina.
- Hash do termo e da evidência.
- CPF criptografado e mascarado.

## Administração

- Site simplificado em URL HTTPS interna.
- Contas administrativas individuais.
- Convites temporários para criação de senha.
- TOTP com Microsoft Authenticator.
- Códigos de recuperação.
- Redefinição controlada do segundo fator.
- Limite diário persistente de tentativas.

## Infraestrutura

- HTTPS nativo.
- Certificados distribuídos pela GPO.
- Migração gradual de URL e porta.
- Compatibilidade temporária durante transição.
- Implantação piloto antes da expansão.

## Decisões importantes

- Não depender de Entra ID Premium.
- Preservar o servidor como autoridade da data e hora.
- Manter o aceite vinculado a usuário e equipamento.
- Não mostrar protocolo ao usuário após a confirmação; preservá-lo no painel, PDF e exportação.
- Não remover evidências sem backup e registro da justificativa.
- Manter repositório técnico privado e livre de dados de produção.

