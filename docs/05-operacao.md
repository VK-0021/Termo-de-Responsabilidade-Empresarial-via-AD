# Operação

## Rotina diária

- Verificar o endpoint `/health`.
- Conferir falhas recentes de aceite.
- Monitorar espaço em disco e execução do backup.
- Tratar chamados de certificado, DNS ou conectividade.

## Rotina semanal

- Revisar novos aceites e inconsistências.
- Validar o download de um PDF de amostra autorizado.
- Conferir administradores ativos e bloqueios de segundo fator.
- Verificar a tarefa do servidor.

## Rotina mensal

- Testar restauração em ambiente isolado.
- Revisar contas administrativas e exceções.
- Confirmar sincronismo de horário.
- Revisar capacidade, logs e retenção.
- Verificar se GPOs antigas permanecem desvinculadas.

## Publicar nova versão do termo

1. Obter aprovação final do Jurídico.
2. Registrar a mudança e a justificativa.
3. Acessar **Versões do termo**.
4. Publicar um identificador de versão único.
5. Confirmar a versão ativa pelo `/health`.
6. Testar na OU piloto.
7. Comunicar que todos os usuários e equipamentos precisarão aceitar novamente.

## Contas administrativas

- Utilizar contas individuais no padrão institucional.
- Cada administrador cria a própria senha.
- TOTP é obrigatório.
- Links de convite são individuais, de uso único e temporários.
- Códigos de recuperação não devem ser compartilhados.
- Redefinir o segundo fator somente após validar a identidade do solicitante.

## Revogação e correção de aceite

Alterações em evidências são ações excepcionais. Antes de revogar ou arquivar:

1. exportar ou preservar a evidência necessária;
2. criar backup consistente do banco;
3. registrar solicitante, motivo, data e executor;
4. afetar somente o usuário e equipamento pretendidos;
5. validar o servidor após a operação.

Não editar o banco manualmente enquanto o serviço estiver gravando.

## Modos de falha

- `open`: registra indisponibilidade e libera a sessão. Indicado para piloto ou conectividade instável.
- `closed`: bloqueia a sessão quando a validação não está disponível. Usar somente após redundância e testes.

