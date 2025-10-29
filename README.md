# Sistema de Estacionamento / Rotativo

Este projeto implementa um **sistema de estacionamento rotativo** utilizando **HTML, CSS e JavaScript puro**, com foco em **programação funcional**.

A aplicação permite registrar entradas e saídas de veículos, configurar faixas de tarifa, adicionais noturnos, valores de pernoite e planos de mensalistas. O sistema calcula automaticamente o valor total por veículo, apresenta o detalhamento por faixa de tempo e exibe métricas gerais como **ocupação média** e **total arrecadado**.

---

## 🚗 Funcionalidades principais

* Cadastro de **entradas e saídas** com data e hora.
* Configuração de **faixas de tarifa** (minutos e valores).
* **Arredondamento por blocos** de tempo (ex.: 15 min, 30 min, 1h).
* Aplicação de **teto diário** e **adicional noturno**.
* Opção de **pernoite** e valor específico.
* **Mensalistas** com limite de plano e **PNEs isentos** (configurável).
* Geração de **relatórios** e **exportação para CSV**.
* Cálculo de **ocupação média** e verificação de **invariantes**:

  * `total ≥ 0`
  * `mensalista não excede teto do plano`

---

## 🧠 Conceitos de Programação Funcional aplicados

A implementação foi construída seguindo princípios da **programação funcional**, priorizando **imutabilidade** e **funções puras**:

| Conceito                 | Aplicação no código                                                                                                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Funções puras**        | Todas as funções de cálculo (`calcFeeByBands`, `roundDurationMinutes`, `includesNight`, `averageOccupancy`, `evaluateAll`) não têm efeitos colaterais e dependem apenas de seus parâmetros. |
| **Imutabilidade**        | O estado global `STATE` nunca é alterado diretamente; novas versões são criadas com `Object.assign()` para evitar mutação.                                                                  |
| **Map/Filter/Reduce**    | Utilizados amplamente para processar listas, como o cálculo de totais, faixas de preço e ocupação média.                                                                                    |
| **Composição funcional** | Funções pequenas e puras são combinadas para formar operações mais complexas.                                                                                                               |
| **Validação funcional**  | A função `validateRecord()` retorna um objeto com `ok` e `errors` sem alterar o registro original.                                                                                          |

Esses conceitos tornam o sistema **previsível, modular e mais fácil de testar e manter**.

---

## 🧩 Estrutura de arquivos

```
📁 estacionamento-rotativo/
├── estacionamento.html   # Aplicação completa (HTML/CSS/JS)
├── README.md             # Este arquivo de documentação
```

---

## 🖥️ Como executar

1. **Baixe o arquivo** `estacionamento.html`.
2. **Abra o arquivo** no navegador (duplo clique ou arraste para uma aba do Chrome, Edge, etc.).
3. Nenhuma instalação adicional é necessária — tudo roda localmente.

---

## 🧾 Exemplo de uso

### Configuração inicial

```
Faixas: 15:2.00;60:5.00;120:9.00;99999:20.00
Arredondamento: 15 min
Teto diário: 35.00
Adicional noturno: R$ 5.00 (22h–06h)
Pernoite: R$ 10.00
```

### Exemplo de entrada

```
Placa: ABC-1234
Tipo: Regular
Entrada: 2025-10-29T08:00
Saída: 2025-10-29T10:30
Pernoite: Não
```

### Saída esperada

```
Tempo total: 150 min
Tempo arredondado: 150 min
Breakdown:
  - 15min → R$ 2.00
  - 60min → R$ 5.00
  - 75min → R$ 5.63 (proporcional)
Total: R$ 12.63
```

### Outro exemplo: PNE isento

```
Placa: XYZ-9999
Tipo: PNE
Entrada: 2025-10-29T09:00
Saída: 2025-10-29T11:00
→ Total: R$ 0.00 (isento)
```

---

## 📊 Relatórios

Após adicionar múltiplos registros, clique em **"Calcular totais"** para gerar:

* **Tabela detalhada** com tempo, tarifas e total por veículo.
* **Resumo geral**:

  * Total arrecadado.
  * Ocupação média (veículos ativos simultaneamente).
  * Contagem de mensalistas.
* **Verificação de invariantes**.

Também é possível **exportar os resultados para CSV** com um clique.

---

## ✅ Invariantes verificadas

Durante o cálculo, o sistema confirma:

* `total ≥ 0` — nunca há valor negativo.
* `mensalista não excede teto do plano` — todos respeitam o limite do plano configurado.

---

## 📚 Créditos

Desenvolvido por **[Aluno]**.
Gerado e comentado com auxílio da **IA (ChatGPT)**.
Implementação totalmente em **JavaScript funcional**, com HTML e CSS integrados para execução direta no navegador.
