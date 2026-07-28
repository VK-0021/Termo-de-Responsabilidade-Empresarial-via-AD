# Implantação

## Pré-requisitos

- Windows Server suportado.
- Node.js homologado ou runtime fornecido com a aplicação.
- DNS interno.
- Certificado TLS para `<URL-TERMOS>`.
- Compartilhamento de implantação acessível pelas contas de computador.
- Backup protegido.
- Conta de emergência definida.

## Sequência recomendada

1. Preparar servidor e diretórios.
2. Instalar a tarefa do servidor.
3. Inicializar configuração com senha forte.
4. Configurar DNS e HTTPS.
5. Distribuir a autoridade certificadora pela GPO.
6. Validar o endpoint de saúde.
7. Publicar a versão inicial do termo.
8. Implantar em uma OU piloto.
9. Validar evidências, PDF e comportamento no logon.
10. Expandir por ondas.

## Verificação do servidor

```powershell
Invoke-RestMethod "https://<URL-TERMOS>/health"
```

Resultado esperado:

```text
status     : ok
activeTerm : <VERSAO-ATIVA>
```

## Configuração

O arquivo de produção contém segredos necessários à API, sessão, criptografia de dados pessoais e HTTPS. Ele deve:

- ficar fora do Git;
- permitir acesso somente à conta do serviço e administradores autorizados;
- fazer parte do backup;
- nunca ser enviado por e-mail, chat ou issue.

## Publicação inicial

No painel:

1. autenticar com conta administrativa;
2. configurar TOTP quando solicitado;
3. acessar **Versões do termo**;
4. informar versão, título e conteúdo revisado;
5. publicar e ativar;
6. confirmar o hash exibido;
7. testar com uma conta comum na OU piloto.

## Gate para produção

- DNS resolvendo nos controladores utilizados pelos clientes.
- Certificado sem aviso de confiança.
- Endpoint de saúde disponível.
- Backup testado.
- Conta de emergência validada.
- GPO aplicada somente ao piloto.
- Cliente consegue registrar e consultar um aceite.
- PDF apresenta o texto e os identificadores esperados.

