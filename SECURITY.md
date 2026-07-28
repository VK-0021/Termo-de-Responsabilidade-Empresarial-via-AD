# Política de segurança do repositório

## Classificação

**Uso Interno Confidencial.** O repositório deve ser privado e acessível apenas à equipe autorizada.

## Conteúdo proibido

Não adicionar dados ou arquivos originados de produção, incluindo:

- `server/data/`;
- `config.json`;
- bancos SQLite e arquivos auxiliares;
- certificados, chaves privadas e senhas;
- chaves de API e segredos de sessão;
- exportações de aceites;
- PDFs de evidência;
- logs de clientes ou servidor;
- capturas de tela com dados pessoais ou infraestrutura identificável;
- nomes, contas, CPFs, SIDs, IPs, seriais, UUIDs e patrimônios reais.

## Procedimento antes do push

1. Revisar os arquivos alterados:

   ```powershell
   git status --short
   git diff --staged
   ```

2. Procurar padrões sensíveis:

   ```powershell
   git grep -n -I -E "apiKey|sessionSecret|adminPasswordHash|BEGIN .*PRIVATE KEY"
   git grep -n -I -E "[0-9]{3}\.[0-9]{3}\.[0-9]{3}-[0-9]{2}"
   git grep -n -I -E "([0-9]{1,3}\.){3}[0-9]{1,3}"
   ```

3. Confirmar que somente exemplos e placeholders aparecem.
4. Solicitar revisão de outro integrante da TI em mudanças de segurança, autenticação, evidência ou GPO.

## Se um segredo for publicado

1. Tornar o repositório inacessível ou suspender o compartilhamento.
2. Revogar imediatamente o segredo exposto.
3. Gerar uma nova chave ou credencial.
4. Remover o conteúdo de todo o histórico Git, não apenas do commit mais recente.
5. Verificar logs de acesso e registrar o incidente.
6. Comunicar o responsável por segurança da informação.

## Comunicação de vulnerabilidades

Não abrir issue pública. Registrar uma issue privada com:

- descrição resumida;
- impacto;
- versão afetada;
- evidência sem dados pessoais;
- contenção aplicada;
- responsável e prazo.

