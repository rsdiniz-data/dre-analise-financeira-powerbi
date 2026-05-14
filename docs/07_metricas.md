# 7. Métricas e Indicadores (DAX)

## 🎯 Objetivo
Desenvolver métricas financeiras em DAX para análise da DRE, permitindo comparações históricas, análises de eficiência e simulações de cenários.

> “O modelo analítico possui um conjunto de medidas DAX responsáveis pelo cálculo dos principais indicadores financeiros.”

---

## 📊 Indicadores Financeiros
KPIs implementados no modelo:

- Receita Bruta  
- Custos  
- Despesas  
- Margem Bruta  
- EBIT  
- EBITDA  
- Lucro Líquido  

Cada métrica utiliza a estrutura contábil da DRE para garantir consistência e rastreabilidade.

---

## 📈 Análises Financeiras
O modelo inclui análises comparativas e gerenciais:

- **YoY** (Year over Year)  
- **AH** (Análise Horizontal)  
- **AV** (Análise Vertical)  
- Variações absolutas e percentuais  
- Comparações entre exercícios  

Essas análises permitem identificar tendências, desvios e evolução da performance financeira.

---

## 🔮 Simulações (What-If)
Simulações foram implementadas para avaliar impactos financeiros em:

- Receita  
- Custos  
- Despesas  
- Margem  
- EBIT  

> “Permite testar hipóteses e antecipar efeitos financeiros de decisões operacionais, comerciais ou de estrutura de custos.”

---

## ⚙️ Medidas Auxiliares
Incluem funcionalidades para:

- Direção de indicadores  
- Formatação executiva  
- Exibição contextual de filtros  
- Conversão de valores para leitura gerencial  

Essas medidas aprimoram a comunicação executiva e a interpretação dos resultados.

---

## 💻 Organização das Medidas DAX
As medidas foram organizadas em arquivos temáticos:

- [01_base.md](../scripts/dax/01_base.md)
- [02_kpis.md](../scripts/dax/02_kpis.md)
- [03_analises.md](../scripts/dax/03_analises.md)
- [04_yoy_valor.md](../scripts/dax/04_yoy_valor.md)
- [05_yoy_percentual.md](../scripts/dax/05_yoy_percentual.md)
- [06_simulacoes.md](../scripts/dax/06_simulacoes.md)
- [07_auxiliares.md](../scripts/dax/07_auxiliares.md) 

📄 Ver visão completa:
👉 [Explorar documentação DAX](../scripts/dax/README.md)

---

## 📷 Indicadores no Dashboard
![Indicadores Financeiros](../images/cartoes_executivos_indicadores_financeiros.png)

---

## 🔗 Rastreabilidade
As métricas estão conectadas diretamente à:

- Modelagem dimensional  
- Estrutura da DRE  
- Regras contábeis  
- Scripts DAX  

Fluxo completo:  
**Fonte de Dados → Transformação → Modelagem → Métricas → Dashboard**
