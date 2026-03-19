# FarmTech Solutions — Fase 5

**Aluno:** Cloves Silva Filho  
**RM:** 567250  
**Grupo:** 21  
**Curso:** Machine Learning, IA Generativa e NLP — FIAP

---

## Sobre o projeto

Esse repositório tem as duas entregas obrigatórias da Fase 5. O objetivo geral foi usar Machine Learning pra analisar dados de safras agrícolas e também comparar custos de hospedagem na AWS pra colocar o modelo em produção.

---

## Arquivos

```
├── ClovesFilho_rm567250_pbl_fase4.ipynb   ← notebook com toda a análise
├── crop_yield.csv                          ← dataset usado
└── README.md                               ← esse arquivo
```

---

## Entrega 1 — Machine Learning

### Notebook

👉 [ClovesFilho_rm567250_pbl_fase4.ipynb](./ClovesFilho_rm567250_pbl_fase4.ipynb)

O notebook tem todo o passo a passo com explicações em markdown. Basicamente fiz três coisas:

- **Análise exploratória** — histogramas, boxplots, mapa de correlação e pairplot pra entender o dataset antes de qualquer modelo
- **Clusterização com K-Means** — usei o método do cotovelo pra escolher k=4, visualizei com PCA e identifiquei outliers pela distância ao centróide
- **5 modelos de regressão** — Regressão Linear, Ridge, Random Forest, Gradient Boosting e SVR, todos avaliados com MAE, RMSE e R²

Os modelos ensemble (Random Forest e Gradient Boosting) tiveram o melhor resultado. A variável mais importante foi o tipo de cultura, o que faz sentido dado que as plantas têm rendimentos completamente diferentes entre si.

### Vídeo

> 📺 [Assistir no YouTube]([https://youtube.com/SEU_LINK_AQUI](https://youtu.be/duZiSH3k5ms))  
> *(não listado, até 5 minutos)*

---

## Entrega 2 — AWS

### O que foi feito

Usei a calculadora da AWS pra comparar o custo de uma instância EC2 Linux entre as regiões de São Paulo (BR) e Virgínia do Norte (EUA), com as configurações pedidas:

| Configuração | Valor |
|---|---|
| CPUs | 2 vCPUs |
| Memória | 1 GiB RAM |
| Rede | até 5 Gigabit |
| Armazenamento | 50 GB |
| OS | Linux |
| Preço | On-Demand 100% |

A instância que se encaixa nessas specs é a **t3.micro**.

### Resultado da comparação

| | São Paulo (sa-east-1) | Virgínia do Norte (us-east-1) |
|---|---|---|
| EC2 t3.micro | ~US$ 12,85/mês | ~US$ 8,35/mês |
| EBS gp3 50 GB | ~US$ 4,00/mês | ~US$ 4,00/mês |
| **Total** | **~US$ 16,85/mês** | **~US$ 12,35/mês** |

*Valores consultados na AWS Pricing Calculator em março/2026.*

```
Comparativo visual (custo mensal):

São Paulo (BR)   ██████████████████  ~$16,85
Virgínia (EUA)   ████████████████    ~$12,35

Diferença: ~$4,50/mês (São Paulo ~36% mais caro)
```

### Qual região escolher?

**Escolhi São Paulo**, mesmo sendo mais caro. Os motivos são:

**Latência** — os sensores da fazenda estão no Brasil. Colocar a API em São Paulo reduz o tempo de resposta entre o sensor e o servidor, o que é importante pra um sistema de monitoramento em tempo real.

**LGPD** — a Lei Geral de Proteção de Dados (Lei 13.709/2018) cria restrições pro armazenamento de dados fora do Brasil. Mesmo que os dados dos sensores não sejam dados pessoais em si, qualquer integração com dados de produtores ou funcionários estaria sujeita à lei. Manter no Brasil evita esse problema.

**Custo** — a diferença de ~$4,50 por mês não justifica abrir mão das vantagens acima. Além disso, dá pra reduzir o custo usando instâncias Reserved no futuro.

### Vídeo

> 📺 [Assistir no YouTube](https://youtube.com/SEU_LINK_AQUI_2)  
> *(não listado, até 5 minutos mostrando a calculadora AWS)*

---

## Como rodar o notebook

1. Coloque o arquivo `crop_yield.csv` na mesma pasta do notebook
2. Instale as dependências:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```
3. Abra o notebook:
```bash
jupyter notebook ClovesFilho_rm567250_pbl_fase4.ipynb
```
