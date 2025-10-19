# 🧠 Anticipatory Shipping Quinzenal

Este projeto utiliza **modelos de previsão Prophet** para estimar a **demanda quinzenal de produtos** e decidir **quais itens devem ser enviados antecipadamente** para cada região da Espanha, antes mesmo da compra ocorrer.

A ideia é simular um sistema de **“envio antecipado inteligente”**, reduzindo tempo de entrega e melhorando a disponibilidade de estoque.  
O modelo combina **análise temporal (quinzenal)**, **percentis de demanda previstos** e **regras de confiança**, resultando em duas decisões possíveis:

- `ENVIAR_ANTES` → estoque recomendado para envio antecipado.  
- `AGUARDAR` → manter estoque atual e aguardar mais sinal de demanda.

---

📊 **Principais tecnologias**  
- Python  
- Prophet (Meta)  
- Pandas / NumPy  
- Tqdm

📂 **Saída principal**  
- `recomendacoes_pre_envio.csv` → contém previsões e decisão final (`ENVIAR_ANTES` ou `AGUARDAR`)

---

👤 **Autor**  
**Alisson Silva Silva**  
Analista de Dados — Espanha 🇪🇸  
[GitHub @alisson-silva92](https://github.com/alisson-silva92)
