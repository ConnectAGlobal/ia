**ConnectA — Integração de IA**

ConnectA é um aplicativo backend desenvolvido em Java com Spring Boot que suporta funcionalidades de assistente inteligente para análise e sugestão a partir de currículos. O projeto foi realizado em grupo e inclui integração com serviços de IA para processar entradas em diferentes idiomas e retornar perfis/skills sugeridas.

**Propósito**: Fornecer um endpoint capaz de receber um currículo em texto e um código de idioma (por exemplo `pt-BR`, `es-ES`) e retornar um perfil assistente com skills, sugestões e informações extraídas automaticamente usando modelos de IA.

**Como funciona (visão geral)**
- **Entrada**: JSON com as chaves `curriculo` e `idioma` (ex.: `{"curriculo":"...","idioma":"pt-BR"}`).
- **Processamento**: O backend envia o texto para o componente de IA (local ou externo) que realiza parsing, extração de skills, sumarização e normalização do idioma.
- **Saída**: JSON com o perfil/skills sugeridas, mensagens de erro quando necessário e dados adicionais conforme a implementação em `AssistenteController`.

**Exemplos de payload (fornecidos pelo grupo)**n+
Exemplo 1 (português):
```
{
  "curriculo": "João Silva, 28 anos. Graduado em Ciência da Computação pela USP. Experiência de 5 anos como Desenvolvedor Full Stack. Domínio de Java, Spring Boot, React, Node.js, TypeScript, PostgreSQL e MongoDB. Experiência com Docker, Kubernetes e CI/CD. Desenvolveu APIs RESTful escaláveis e aplicações web responsivas. Conhecimento em AWS e Azure. Trabalhou em projetos ágeis usando Scrum. Soft skills: comunicação eficaz, trabalho em equipe, resolução de problemas, adaptabilidade e liderança técnica.",
  "idioma": "pt-BR"
}
```

Exemplo 2 (espanhol):
```
{
  "curriculo": "María García, 26 años. Licenciada en Diseño Gráfico. 4 años de experiencia como Diseñadora UX/UI. Experta en Figma, Adobe XD, Sketch, Photoshop e Illustrator. Experiencia en investigación de usuarios, prototipado, design thinking y arquitectura de información. Creación de design systems y componentes reutilizables. Conocimientos de HTML, CSS y JavaScript básico. Trabajo colaborativo con equipos de desarrollo. Habilidades: creatividad, empatía, pensamiento crítico, atención al detalle.",
  "idioma": "es-ES"
}
```

Exemplo 3 (português - gestão):
```
{
  "curriculo": "Ana Paula Costa, 35 anos. MBA em Gestão de Projetos pela FGV. Certificações PMP e Scrum Master. 8 anos de experiência gerenciando projetos de tecnologia. Expertise em metodologias ágeis (Scrum, Kanban) e tradicionais (PMBOK). Gestão de orçamentos de até R$ 5 milhões. Liderança de equipes multidisciplinares de até 20 pessoas. Conhecimento em Jira, Trello, MS Project e Asana. Inglês fluente. Soft skills: liderança, negociação, comunicação estratégica, gestão de conflitos, tomada de decisão.",
  "idioma": "pt-BR"
}
```

Exemplo 4 (português - dados):
```
{
  "curriculo": "Carlos Mendes, 30 anos. Bacharel em Estatística. 6 anos como Analista de Dados. Especialista em Python, R, SQL, Power BI e Tableau. Experiência com machine learning usando scikit-learn e TensorFlow. Análise estatística avançada, modelagem preditiva e visualização de dados. Trabalhou com big data usando Spark e Hadoop. Conhecimento de Cloud (AWS, GCP). Desenvolveu dashboards interativos e relatórios executivos. Skills: análise crítica, storytelling com dados, atenção a detalhes, curiosidade analítica.",
  "idioma": "pt-BR"
}
```

**Observação importante sobre rotas/uso**
- Consulte o controller `AssistenteController` em `src/main/java/.../controller` para confirmar a rota exata que processa currículos (por exemplo, um endpoint POST que recebe o JSON acima).
- Exemplo genérico de uso (ajuste a rota conforme seu controller):
```
curl -X POST "http://localhost:8080/assistente/processar" \
  -H "Content-Type: application/json" \
  -d '{"curriculo":"...","idioma":"pt-BR"}'
```

**Rodando o projeto localmente**
- Instalar JDK compatível (ver `pom.xml` para versão recomendada).
- No Windows (PowerShell), rodar em modo desenvolvimento:
```
.\mvnw.cmd spring-boot:run
```
- Para buildar o jar e executar:
```
.\mvnw.cmd clean package
java -jar target\*.jar
```

**Docker**
- Build da imagem:
```
docker build -t connecta .
```
- Rodar container:
```
docker run -p 8080:8080 --env-file .env connecta
```

**Ambiente / Configurações**
- As configurações estão em `src/main/resources/application.properties` e o projeto também inclui `DotenvConfig` para carregar variáveis de ambiente de um arquivo `.env` quando necessário.
- Variáveis comuns: chaves/URLs de serviços de IA, configurações de RabbitMQ, segurança JWT, etc. Confira `src/main/java/.../config` para detalhes.

**Testes**
- Rodar testes unitários:
```
.\mvnw.cmd test
```

**Créditos (Trabalho em grupo)**
- Pedro Henrique dos Santos — RM `559064`
- Vinícius de Oliveira Coutinho — RM `556182`
- Thiago Thomaz Sales Conceição — RM `557992`

**Contexto do app (sugestão de início para documentação)**
- ConnectA é um aplicativo originalmente pensado para conectar mentores e mentorados, promovendo aprendizado colaborativo e inclusão digital. Nesta implementação, a componente de IA ajuda a analisar currículos, gerar perfis de assistentes/mentores e sugerir skills e compatibilidades automaticamente.

**Próximos passos sugeridos**
- Documentar rotas REST específicas em `AssistenteController`, `AuthController` e `UsuarioController`.
- Incluir exemplos de respostas da API (formatos de `JwtResponseDTO`, `UsuarioResponseDTO` e `SkillsSugeridasDTO`).
- Adicionar um pequeno guia de como trocar o provedor de IA (local vs externo) e exemplos de variáveis `.env` necessárias.

---
Se quiser, eu adapto o README para inglês, gerarei exemplos de respostas da API, ou documentarei rotas específicas com base no código fonte (posso extrair as anotações `@RequestMapping` automaticamente). Quer que eu faça isso agora?
