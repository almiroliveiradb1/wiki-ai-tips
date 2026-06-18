# Tri-Track Agile — As Três Trilhas

O Tri-Track Agile (ou Agile de Três Trilhas) é uma evolução do conhecido Dual-Track Agile (que divide o trabalho em Descoberta/Discovery e Entrega/Delivery).
No Tri-Track, adiciona-se uma terceira trilha dedicada exclusivamente à Estratégia e Alinhamento de Negócios. Isso garante que o time não apenas descubra como fazer e entregue rápido, mas que esteja construindo a coisa certa para os objetivos da empresa de longo prazo.
As três trilhas rodam de forma paralela e contínua, alimentando umas às outras.
As Três Trilhas
[ Trilha 1: Estratégia / Validação de Negócio ] (O "Porquê")
↓
[ Trilha 2: Product Discovery / Descoberta ]   (O "O quê")
↓
[ Trilha 3: Product Delivery / Entrega ]       (O "Como")
## 1. Trilha de Estratégia (Strategy Track)
Foco: O "Porquê".
O que faz: Olha para o mercado, objetivos de negócio (OKRs), feedback de alto nível e viabilidade financeira. Define quais problemas macro valem a pena ser resolvidos.
Quem participa: Product Directors, Stakeholders, C-Level e Tech Leads.
## 2. Trilha de Descoberta (Discovery Track)
Foco: O "O quê".
O que faz: Pega os problemas validados pela estratégia e vai entender o usuário. Aqui acontecem pesquisas, entrevistas, desenhos de arquitetura técnica preliminar, prototipagem e testes de usabilidade. O objetivo é mitigar riscos antes de escrever código.
Quem participa: Product Managers (PMs), Product Designers (UX/UI) e Tech Leads/Engenheiros seniores.
## 3. Trilha de Entrega (Delivery Track)
Foco: O "Como".
O que faz: É o desenvolvimento ágil tradicional (Scrum/Kanban). Pega o que foi validado no Discovery e transforma em software pronto para produção, com foco em qualidade, arquitetura limpa, testes automatizados e deploy.
Quem participa: Engenheiros de Software, QA e o time de desenvolvimento como um todo.
Exemplo Prático: Implementando um Sistema de Recomendações por IA
Imagine que um e-commerce quer aumentar o faturamento integrando um sistema inteligente de sugestões de produtos. Veja como as três trilhas trabalham juntas na mesma semana:
Na Trilha de Estratégia (Pensando no trimestre/ano)
O time de negócios analisa que o ticket médio caiu 15%. Eles definem a meta (OKR): Aumentar o valor médio do carrinho em 20% usando inteligência artificial.
Eles avaliam o orçamento para infraestrutura de nuvem (como custos de LLMs ou modelos de machine learning) para garantir o retorno sobre o investimento (ROI).
Na Trilha de Descoberta (Pensando nas próximas semanas)
Enquanto o time de engenharia desenvolve outras tarefas, o PM e o Designer criam protótipos de tela mostrando onde as recomendações vão aparecer (na página do produto? no carrinho?).
O Tech Lead estuda quais APIs ou serviços de IA (como soluções serverless ou filas de mensageria para processamento assíncrono) atendem à volumetria necessária sem estourar o tempo de resposta da página. Eles validam o layout com usuários reais.
Na Trilha de Entrega (Pensando na Sprint atual)
O time de desenvolvimento está codificando os componentes de interface que já foram validados no Discovery há duas semanas.
Eles criam os microsserviços necessários, estruturam os contratos de API, escrevem testes unitários e preparam as esteiras de CI/CD para colocar a primeira versão simples (MVP) no ar.
A grande vantagem: O time de engenharia nunca fica "bloqueado" esperando o design ou a definição de negócio, e o time de negócio nunca define algo que é impossível ou caro demais para a engenharia construir, pois há um fluxo contínuo de informação entre as trilhas.

