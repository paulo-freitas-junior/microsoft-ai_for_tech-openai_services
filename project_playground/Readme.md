# Azure OpenAi no Playground
## Base e Setup do Azure OpenAI

Este documento é um resumo compilado do desafio de projeto proposto, onde estão os principais tópicos abordados no vídeo do projeto e um resumo de cada ponto apresentado.

---
## 1. Setup e Configuração do Azure OpenAI
O processo de configuração envolve:
- **Criação de um recurso do Azure OpenAI** na plataforma Azure. Para isso, é necessário ter uma assinatura ativa.
- Definir os **parâmetros regionais e de disponibilidade**, verificando se o recurso está habilitado para a localização do usuário.
- Configurar as **chaves de acesso e endpoints** necessários para a autenticação.
- Integrar o Azure OpenAI com outros serviços, como APIs e ferramentas adicionais.

---

## 2. Deploy
O deploy refere-se à ativação de modelos OpenAI dentro do Azure. Etapas principais:
- Escolher o modelo pré-treinado adequado, como **GPT-4**, **Codex** ou outro, dependendo das necessidades do projeto.
- Configurar o **SKU de escalabilidade** para garantir desempenho otimizado.
- Monitorar o **uso e custos** para alinhar às limitações do projeto.
  
---

## 3. O que é um Playground no Azure
O Playground é uma interface interativa oferecida no Azure OpenAI para:
- **Testar modelos:** Experimente diferentes modelos de IA para tarefas como geração de texto, criação de imagens e muito mais.
- **Ajustar parâmetros:** Como temperatura, frequência e presença de penalização de forma prática. Personalize as configurações para obter os resultados desejados.
- **Integrar dados próprios:** Use seus próprios dados para treinar e ajustar os modelos, tornando-os mais relevantes para o seu caso de uso.
- **Simular interações:** Teste como os modelos respondem a diferentes entradas em um ambiente controlado.
- **Permitir a prototipação** de solicitações antes de implementar as APIs em produção.

---

## 4. Quais os Recursos do Playground
- **Interface de fácil uso** para prototipagem.
- Testes com diferentes **modelos linguísticos e parâmetros ajustáveis**.
- Ferramentas para exportar configurações para uso direto via API.
- Visualização dos resultados em tempo real para diferentes entradas de texto.
Os modelos de linguagens são estocáticos, que dependem muito do acaso, ou seja, dependem dos parâmetros que são inseridos.


### Parâmetros de configurações:
	- Temperatura
	- Top P
	- Tokens Máximos
	- Penalidades
	- Sistemas de mensagens


---

## 5. Como é feito o processo de Tokenização
- A tokenização converte texto em unidades menores chamadas **tokens**.
- Para modelos OpenAI, tokens podem representar caracteres, palavras ou parte de palavras, dependendo do idioma.
- A contagem de tokens afeta custos e desempenho, sendo essencial otimizar entradas para reduzir o uso excessivo.
- Palavras em inglês geralmente consomem menos Tokens tanto na entrada como no resultado, sendo recomendado sempre quando possível gerar os prompts em inglês, porém será necessário especificar o idioma de saída no prompt caso seja em outro idioma.
Adotar técnicas de engenharia de prompt bem definidas, ajudam a minimizar o consumo de tokens, principalmente se aplicar métodos de **divisão de tarefas complexas**.
Dependendo do modelo de linguagem que é escolhido e da região que se é escolhida, os valores de cobrança são diferenciados para cada **1M Tokens.**


---

## 6. O que é o System Message
O **System Message** é uma mensagem inicial enviada aos modelos OpenAI para:
- **Contexto inicial**.
- **Definir o comportamento ou estilo de resposta do modelo**.
- **Instruções de base**.
    - Por exemplo, pode-se instruir o modelo a responder como um especialista em medicina ou um professor universitário.
    - Essa configuração inicial é fundamental para alinhar a saída com os requisitos do usuário.
### Aplicação de Técnica de Engenharia de Prompts
	- Instruções claras e objetivas
	- Aplicação do GuardRails
	- Preparo da saída do modelo
	- Solicitação de Cadeia de Pensamento do modelo
	- Especificar a Estrutura de Saída
	- Divisão das Tarefas Complexas do Prompt
	- Uso de Sintaxes claras
#### ZERO-SHOT
- Sem exemplos
- Resposta direta
- Baseada apenas no prompt

#### ONE-SHOT
- Possui um exemplo
- Modelo de lingaguem entende o exemplo de entrada como exemplo de saída
- Não lida com coisas incertas!

---

## 7. Diferenças de Temperatura vs. Top-P
Esses parâmetros ajudam a ajustar a criatividade das respostas:
| **Parâmetro** | **Descrição**                             | **Como equilibrar**                                                |
|---------------|------------------------------------------|-------------------------------------------------------------------|
| **Temperatura** | Controla a aleatoriedade na geração de texto. Valores altos (ex.: 0.8) geram respostas mais criativas; valores baixos (ex.: 0.2) tornam o texto mais objetivo. | Escolha valores baixos para respostas previsíveis e valores altos para maior criatividade. |
| **Top-P**      | Define a probabilidade cumulativa no corte de opções. Um Top-P de 0.9 limita escolhas às mais prováveis. | Use em conjunto com Temperatura para refinar o equilíbrio entre criatividade e coerência.  |

Ajustar os parâmetros de **temperatura** e **top-p** permite personalizar o equilíbrio entre criatividade e previsibilidade nos resultados gerados. 

### Temperatura
- **Baixa Temperatura (0.1–0.3):** Torna as respostas mais previsíveis e focadas, adequadas para tarefas onde precisão e consistência são prioritárias, como instruções técnicas ou conteúdo acadêmico.
- **Temperatura Média (0.4–0.7):** Oferece um equilíbrio entre criatividade e precisão, ideal para respostas semi-estruturadas, como e-mails ou sugestões criativas moderadas.
- **Alta Temperatura (0.8–1.0):** Gera respostas mais criativas e variadas, útil para brainstorming, criação de histórias ou conteúdo artístico. Contudo, pode resultar em menor coerência.

### Top-P (Probabilidade Cumulativa)
- **Baixo Top-P (0.1–0.5):** Restringe as escolhas às opções mais prováveis, tornando as respostas mais consistentes e focadas.
- **Médio Top-P (0.6–0.8):** Permite certa flexibilidade, gerando respostas criativas, mas ainda coerentes.
- **Alto Top-P (0.9–1.0):** Aumenta a diversidade e expande as possibilidades das respostas, permitindo que o modelo explore opções menos óbvias.


### Como Equilibrar
- Para um resultado mais estruturado e confiável, use **temperatura baixa** em conjunto com **top-p médio a baixo**.
- Para um equilíbrio, combine **temperatura média** com **top-p médio**.
- Para explorar ideias ou criatividade máxima, utilize **temperatura alta** com **top-p alto**, mas monitore se o conteúdo ainda faz sentido.
Os parâmetros **temperatura** e **top-p** podem ser ajustados de forma independente, mas eles se influenciam mutuamente no comportamento do modelo, principalmente na diversidade e coerência das respostas geradas. 

### Influência Recíproca
1. **Temperatura Alta + Top-P Baixo:**
   - A alta temperatura incentiva o modelo a explorar opções menos prováveis, mas o top-p baixo limita essa exploração às escolhas mais prováveis.
   - O resultado é uma geração de texto ainda previsível, porém com pequenas variações criativas.

2. **Temperatura Baixa + Top-P Alto:**
   - A baixa temperatura restringe a aleatoriedade, mas o top-p alto permite que o modelo considere uma ampla gama de probabilidades.
   - Isso pode levar a respostas mais variadas, mas ainda controladas pela redução da aleatoriedade.

3. **Temperatura Alta + Top-P Alto:**
   - Ambos os parâmetros incentivam a criatividade e a diversidade. Isso pode resultar em respostas altamente originais, mas também em uma maior chance de incoerência ou irrelevância.
   - Essa configuração é ideal para brainstorming ou exploração criativa, mas requer mais ajustes para melhorar a qualidade.

4. **Temperatura Baixa + Top-P Baixo:**
   - Restringe tanto a criatividade quanto a variabilidade. Essa combinação é útil para cenários onde respostas precisas e consistentes são prioritárias, como instruções técnicas.

| **Temperatura**    |**Top P**    | **Descrição**                          |
|--------------------|-------------|----------------------------------------|
| Alta               | Alta        | Criatividade máxima                    |
| Alta               | Baixa       | Criatividade mais limitada             |
| Baixo              | Alta        | Variedade Controlada                   |
| Baixo              | Baixo       | Máxima previsibilidade                 |


### Considerações Práticas
- A interação entre esses parâmetros depende do uso desejado. Por exemplo:
   - Se deseja maximizar a criatividade, aumentar ambos os valores (temperatura e top-p) será mais eficaz.
   - Se a prioridade for consistência e foco, reduzir ambos os valores garantirá respostas mais controladas.
- Testar diferentes combinações no **Playground do Azure** pode ajudar a encontrar o equilíbrio ideal para cada caso de uso.



---

## 8. Frequency Penalty vs. Presence Penalty
| **Parâmetro**        | **Descrição**                                         | **Uso Prático**                                                   |
|-----------------------|-----------------------------------------------------|-------------------------------------------------------------------|
| **Frequency Penalty** | Penaliza termos repetidos para evitar redundância.   | Ideal para criar textos menos repetitivos.                       |
| **Presence Penalty**  | Penaliza ou favorece termos novos na resposta.       | Útil para incentivar a introdução de novas ideias no texto.      |

### **Frequency Penalty**
- **O que é:** Penaliza a repetição de palavras ou frases no texto gerado.
- **Objetivo:** Reduzir a repetitividade, incentivando o modelo a criar respostas mais diversificadas.
- **Como funciona:** 
  - Aumentando o valor do **Frequency Penalty**, o modelo se torna menos propenso a reutilizar termos que já apareceram no texto.
  - Esse parâmetro é útil em casos onde você deseja evitar redundâncias em respostas longas ou textos criativos.

**Exemplo prático:**
- Sem Frequency Penalty (valor baixo ou zero):
  - "O cachorro corre no parque, e o cachorro está feliz no parque."
- Com Frequency Penalty (valor alto):
  - "O cachorro corre pelo parque, demonstrando felicidade ao brincar."

### **Presence Penalty**
- **O que é:** Ajusta a probabilidade de o modelo introduzir novas palavras ou tópicos no texto.
- **Objetivo:** Incentivar ou limitar a presença de novas ideias ou termos durante a geração do texto.
- **Como funciona:**
  - Aumentando o valor do **Presence Penalty**, o modelo é estimulado a trazer termos ou conceitos novos.
  - Reduzir esse valor faz o modelo permanecer em tópicos previamente discutidos, proporcionando mais consistência.

**Exemplo prático:**
- Sem Presence Penalty (valor baixo ou zero):
  - "O parque estava vazio. O parque parecia calmo e silencioso."
- Com Presence Penalty (valor alto):
  - "O parque estava vazio. Árvores balançavam ao vento, e ao longe se ouviam pássaros cantando."

### **Diferenças e Uso Prático**
| **Parâmetro**        | **Quando usar**                                                                                      | **Resultados**                                                        |
|-----------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| **Frequency Penalty** | Para evitar repetições excessivas em respostas longas ou textos criativos.                          | Gera texto mais variado e menos redundante.                           |
| **Presence Penalty**  | Para encorajar o uso de palavras inéditas ou a introdução de novos temas em uma resposta criativa.  | Incentiva o surgimento de ideias mais originais e diversificadas.     |

### **Usar Juntos ou Separados?**
- **Separadamente:** Se o texto precisar apenas ser menos repetitivo, ajuste o **Frequency Penalty**. Para explorar novos tópicos, aumente o **Presence Penalty**.
- **Combinados:** Para alcançar maior fluidez e criatividade, ajustar ambos pode ser necessário. Por exemplo, valores médios de ambos (como 0.5) garantem equilíbrio entre diversidade e coesão.



---

## 9. Multimodalidade
A multimodalidade no Azure OpenAI refere-se à capacidade de trabalhar com diferentes tipos de dados, como:
- **Texto, imagens e sinais** processados em conjunto.
- Uso de modelos avançados que integram linguagens naturais com visão computacional (ex.: GPT-4 multimodal).
- Aplicações incluem análise de dados complexos, suporte ao design e sistemas de recomendação.

---


