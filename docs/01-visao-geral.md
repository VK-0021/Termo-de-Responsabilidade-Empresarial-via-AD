# Visão geral

## Problema

A organização precisa comprovar que cada colaborador tomou ciência das regras de recebimento e uso dos equipamentos corporativos. O aceite deve acompanhar o usuário e o equipamento, inclusive em computadores compartilhados, sem depender de recursos Premium do Entra ID.

## Solução

Um cliente Windows consulta um servidor interno no logon. Quando não existe evidência para a versão ativa, o cliente apresenta o termo em tela cheia e exige:

1. leitura do conteúdo até o final;
2. declaração explícita de ciência;
3. CPF válido;
4. confirmação do aceite.

O servidor registra a evidência e passa a reconhecer aquela combinação de usuário e equipamento.

## Regra de reapresentação

O termo volta a ser apresentado quando:

- outra pessoa entra no mesmo equipamento;
- o mesmo usuário utiliza outro equipamento;
- uma nova versão do termo é publicada;
- a identidade técnica do equipamento muda após substituição relevante ou formatação;
- o aceite correspondente é revogado administrativamente.

## Exceções

Contas administrativas e contas locais de emergência podem ser dispensadas conforme configuração central. As exceções devem ser mínimas, nominativas ou baseadas em padrão controlado, revisadas periodicamente e auditáveis.

## Critérios de sucesso

- Aplicação automática pela GPO.
- Exibição somente quando houver pendência.
- Impossibilidade de confirmar antes do fim da leitura.
- Registro central com protocolo e hash.
- Consulta, PDF e exportação disponíveis somente para administradores.
- Recuperação documentada em caso de indisponibilidade.

## Limites

O aceite autenticado é evidência eletrônica, mas não equivale automaticamente a uma assinatura eletrônica qualificada. O valor probatório e a redação do termo devem ser definidos pelo Jurídico.

