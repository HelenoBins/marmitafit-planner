# MarmitaFit Planner

Aplicativo web para planejamento semanal de marmitas saudáveis. Em vez de digitar cada prato, a pessoa marca em uma checklist quais itens (proteína, carboidrato, legumes etc.) vai usar em cada dia da semana ao montar as marmitas. A partir das marcações, o sistema calcula automaticamente a **compra programada da semana**, somando a quantidade necessária de cada item conforme o número de vezes que ele foi marcado.

## Tecnologias

- HTML5, CSS3 e JavaScript (checklist semanal e cálculo da lista de compras)
- PHP + MySQL (persistência de dados em `/php`)

## Como funciona

1. O catálogo já vem com itens comuns (carnes, carboidratos, legumes) organizados por categoria, cada um com uma quantidade padrão por marmita (ex.: 150 g de carne moída).
2. A pessoa marca, para cada dia da semana (Seg a Dom) e para Almoço e Jantar separadamente, quais itens vai usar naquela marmita.
3. O painel "Compra programada" soma automaticamente: quantidade por marmita × número de marmitas marcadas (almoço + jantar) na semana, e mostra o total já convertido (ex.: g → kg quando ultrapassa 1000 g).
4. É possível adicionar itens personalizados ao catálogo (outras opções de carne, temperos etc.) e remover os que não são usados.

## Como executar

### Opção 1 — Demonstração rápida (sem servidor)
Basta abrir `index.html` em qualquer navegador. O catálogo e as marcações da semana ficam salvos localmente (localStorage).

### Opção 2 — Com back-end PHP/MySQL
1. Importe `php/schema.sql` em um banco MySQL (já cria as tabelas e insere o catálogo padrão).
2. Ajuste as credenciais em `php/config.php`.
3. Sirva o projeto com um servidor PHP local (ex.: `php -S localhost:8000` na raiz do projeto, ou XAMPP/WAMP).
4. Endpoints disponíveis:
   - `GET /php/listar_itens.php` — lista o catálogo de itens
   - `POST /php/adicionar_item.php` — adiciona um item personalizado
   - `POST /php/marcar_item.php` — marca/desmarca um item em um dia e refeição (`item_id`, `dia_semana` 0-6, `refeicao` "Almoço"/"Jantar", `semana_referencia`, `marcado`)
   - `GET /php/gerar_compra.php?semana_referencia=AAAA-MM-DD` — retorna a compra programada da semana com as quantidades já somadas

## Estrutura

```
marmitafit/
├── index.html          # checklist semanal e cálculo da compra programada
├── README.md
└── php/
    ├── config.php
    ├── schema.sql
    ├── listar_itens.php
    ├── adicionar_item.php
    ├── marcar_item.php
    └── gerar_compra.php
```

## Autoria

Desenvolvido como parte das Atividades Extensionistas, com aplicação prática no planejamento de marmitas para uma usuária real, conforme registrado nas fotos anexadas ao relatório do projeto.
