
# Migração Automatizada de Componentes React para Material UI com LLMs: Um Estudo Experimental

**João Vítor Vaz¹, Victor Hugo Martins¹**  
¹Departamento de Ciência da Computação – Universidade Federal de Minas Gerais (UFMG)  
{joaovitorvaz, victorhm}@dcc.ufmg.br

---

## 1. Introdução

A evolução constante de sistemas web modernos tem impulsionado a adoção de design systems como estratégia de manutenção sustentável e escalável. Ferramentas como o Material UI (MUI) se tornaram fundamentais no ecossistema React por proporcionarem uma padronização visual robusta, componentes reutilizáveis e maior produtividade no desenvolvimento frontend [Boduch 2019].

Contudo, uma parcela expressiva de aplicações legadas ainda utiliza estilos manuais via CSS tradicional, inline styles ou bibliotecas como `styled-components`, o que dificulta a manutenção, reduz a legibilidade do código e compromete a uniformidade visual [Thomas 2020]. A migração desses estilos para um design system como o MUI é, portanto, desejável, mas tipicamente onerosa, sujeita a erros humanos e dependente de conhecimento especializado.

Neste contexto, os Modelos de Linguagem de Grande Escala (LLMs), como o GPT-3.5, têm se destacado por sua capacidade de compreender estruturas de código e gerar transformações coerentes a partir de instruções em linguagem natural [Ye et al. 2023]. Este trabalho propõe avaliar a viabilidade da utilização de LLMs na migração automatizada de componentes React com estilização manual para o Material UI, com foco em atributos de manutenibilidade, aderência ao design system e fidelidade visual.

---

## 2. Trabalhos Relacionados

A manutenção de software, particularmente a refatoração de interfaces, tem sido tradicionalmente abordada com técnicas baseadas em análise de código estático, regras heurísticas e árvores de sintaxe abstrata (ASTs). Refatorações visuais, como a padronização de estilos, são frequentemente negligenciadas por ferramentas automatizadas devido à dificuldade de garantir a fidelidade visual e semântica do código convertido.

Obras clássicas como a de [Fowler 2018] sistematizam padrões de refatoração estruturais e de estilo, enquanto [Lehman 1997] discute a inevitabilidade da mudança em sistemas de software e a necessidade de ferramentas que auxiliem sua evolução contínua. No entanto, essas abordagens não contemplam o uso de modelos de linguagem treinados em larga escala.

Com o avanço dos LLMs, novas possibilidades emergem para automação de tarefas de manutenção. Estudos recentes demonstram a eficácia desses modelos na geração e transformação de código com base em descrições em linguagem natural [Chen et al. 2023], [Zhou et al. 2022]. Entretanto, a maior parte das investigações concentra-se em tarefas como completude de código, correção de bugs ou explicação de trechos, com foco em linguagens back-end como Python ou Java.

Poucos trabalhos abordam o uso de LLMs em refatorações estilísticas com impacto visual, como a migração de componentes React para design systems como o MUI. Além disso, há uma lacuna na análise da qualidade do código gerado sob aspectos como modularidade, aderência a padrões visuais e legibilidade — métricas essenciais no contexto de manutenção evolutiva.

Este trabalho busca preencher essa lacuna ao propor um estudo experimental voltado à migração automatizada de interfaces frontend com LLMs, com avaliação sistemática e orientada a critérios de manutenibilidade e aderência a design systems.

---

## 3. Objetivo

Avaliar empiricamente a eficácia de LLMs na transformação automatizada de componentes React com estilos manuais para versões aderentes ao Material UI. A análise será orientada por critérios de preservação de funcionalidade e aparência, legibilidade do código gerado, modularidade, e aderência às boas práticas do design system.

---

## 4. Metodologia

### 4.1. Modelo de Linguagem

Será utilizado o GPT-3.5, acessado via API oficial da OpenAI. O modelo foi escolhido por sua capacidade comprovada de geração de código e interpretação contextual de instruções. Serão testadas duas abordagens de prompting:

- **Zero-shot prompting:** apenas a instrução de conversão;
- **One-shot prompting:** instrução acompanhada de um exemplo de entrada e saída.

### 4.2. Conjunto de Dados

Será construído um corpus com aproximadamente 30 componentes React estilizados manualmente, representando padrões recorrentes em aplicações web. Os componentes incluirão:

- Formulários (inputs, login, cadastro);  
- Botões com estilização personalizada;  
- Cards com imagem e descrição;  
- Layouts com grid e flexbox;  
- Modais e caixas de diálogo.

**Critérios de seleção:**

- Presença de estilização explícita via CSS, inline ou `styled-components`;  
- Viabilidade de mapeamento para estruturas equivalentes no MUI;  
- Diversidade de propriedades estilísticas (margens, cores, espaçamentos etc.).

---

## 5. Experimentos

### 5.1. Exemplos de Possíveis Prompts a Serem Utilizados

**Zero-shot (exemplo):**  
> “Converta o seguinte componente React, estilizado com CSS manual, para uma versão equivalente utilizando apenas componentes do Material UI (MUI), com uso de `sx` props ou estilização padrão. Mantenha aparência e funcionalidade.”

**One-shot (exemplo):**
```jsx
// Original
<div className="card">...</div>
.card { padding: 16px; }

// Convertido
<Card sx={{ p: 2 }}>...</Card>
```

---

## 6. Avaliação

### 6.1. Avaliação Quantitativa

Serão utilizadas as seguintes métricas computáveis:

- **Redução de uso de CSS:** percentual de linhas CSS eliminadas;
- **Aderência ao MUI:** proporção de elementos convertidos para componentes do design system;
- **Uso correto de props MUI:** uso adequado de `sx`, `variant`, `spacing`, etc.;
- **Erros de renderização:** falhas de compilação ou warnings durante execução.

Métricas serão coletadas por meio de scripts automatizados, uso de ESLint customizado, contadores JSX e logs de build.

### 6.2. Avaliação Qualitativa

Análise por especialistas frontend (avaliadores com experiência em React e MUI), com uso de escala Likert (1 a 5) para os seguintes critérios:

- **Fidelidade visual**: semelhança com o componente original;  
- **Legibilidade do código**: clareza e concisão do JSX gerado;  
- **Modularidade**: capacidade de reutilização e separação de responsabilidades;  
- **Aderência ao design system**: conformidade com práticas do MUI;  
- **Eliminação de estilos manuais**: sucesso na substituição de estilos externos.

Os resultados serão registrados em planilhas estruturadas e analisados estatisticamente.

---

## 7. Contribuições Esperadas

- Estudo empírico sobre a aplicabilidade de LLMs na manutenção evolutiva de software front-end;
- Conjunto de dados público com exemplos de migração manual e automatizada;
- Análise quantitativa e qualitativa sobre os limites atuais de LLMs para refatoração estilística;
- Estratégias de prompting reutilizáveis para tarefas similares.

---

## Referências

- Boduch, A. (2019). *React Material-UI Cookbook*. Packt Publishing.  
- Ye, J., et al. (2023). *A Comprehensive Capability Analysis of GPT-3 and GPT-3.5 Series Models*. arXiv preprint.  
- Fowler, M. (2018). *Refactoring: Improving the Design of Existing Code*. Addison-Wesley.  
- Lehman, M. M. (1997). *Laws of Software Evolution Revisited*. In *Proceedings of the European Workshop on Software Process Technology*.
- Chen, Z., et al. (2023). Codex Performance in Code Translation and Refactoring Tasks. arXiv preprint.
- Zhou, S., et al. (2022). LLMs for Automated Software Engineering: Capabilities and Limitations. EMSE.
- Barr, E. T., et al. (2015). The plastic surgery hypothesis. FSE.
- Kim, M., Zimmermann, T., & Nagappan, N. (2012). Crash graphs: A tool for debugging production failures. ICSE.
- Allamanis, M., Barr, E. T., Bird, C., & Sutton, C. (2018). A Survey of Machine Learning for Big Code and Naturalness. ACM Computing Surveys.
- Thomas, Alice et al. (2020) Framework change for modernization of webservice. 

