# Healthcare Dashboard SQL Dataset

Consulta SQL em BigQuery para consolidar solicitações, itens autorizados, dados cadastrais e informações assistenciais em uma base de apoio a dashboard.

## Objetivo

A query constrói uma visão analítica de atendimentos relacionados a um conjunto específico de serviços de saúde. O fluxo identifica solicitações, traduz status operacionais, encontra o atendimento mais recente por beneficiário e enriquece o resultado com dados cadastrais, prestadores, planos e valores pagos.

## Arquivo

- `QRY_TEA.sql`: consulta principal com tabelas e identificadores anonimizados.

## Etapas da consulta

1. seleciona solicitações e itens dos serviços acompanhados;
2. traduz códigos de status para descrições legíveis;
3. utiliza `ROW_NUMBER` para ordenar atendimentos por beneficiário;
4. identifica o atendimento mais recente;
5. adiciona cadastro, status do plano e perfil etário;
6. enriquece com informações do dashboard assistencial;
7. produz a seleção final para consumo analítico.

## Técnicas SQL demonstradas

- Common Table Expressions;
- joins entre fatos e dimensões;
- window functions;
- criação de flags analíticas;
- categorização de idade;
- tradução de códigos com `CASE`;
- anonimização de referências de infraestrutura.

## Como reutilizar

1. substitua projetos, datasets, tabelas e códigos anonimizados;
2. revise a data de corte;
3. valide a granularidade após cada join;
4. verifique duplicidades antes de materializar a tabela;
5. confirme quais campos pessoais são realmente necessários no dashboard.

## Governança e privacidade

A consulta referencia atributos pessoais, como documentos, nomes e contatos. Em um ambiente produtivo, restrinja o acesso, aplique mascaramento quando possível e exponha ao dashboard somente as colunas necessárias.

## Limitações

- códigos de serviço estão incorporados ao filtro;
- a data de corte está fixa;
- a query depende de estruturas específicas do ambiente original;
- não há testes de qualidade ou contagem de duplicidades neste repositório;
- a seleção final pode ser reduzida para evitar exposição desnecessária de dados pessoais.

## Evolução recomendada

- parametrizar período e códigos de serviço;
- criar testes de unicidade por beneficiário e atendimento;
- documentar a granularidade esperada da saída;
- separar uma camada restrita com PII de uma camada analítica anonimizada.