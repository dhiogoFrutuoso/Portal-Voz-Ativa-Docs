# Portal Voz Ativa — Documentação e Arquitetura

![Visibilidade](https://img.shields.io/badge/Reposit%C3%B3rio-Documental%20(Sem%20C%C3%B3digo)-1351B4?style=for-the-badge)
![Plataforma](https://img.shields.io/badge/Plataforma-Web--App-blue?style=for-the-badge)
![Campeão](https://img.shields.io/badge/Campe%C3%A3o%20Estadual-Cear%C3%A1%20de%20Valores-FFD700?style=for-the-badge)
![Licença](https://img.shields.io/badge/Licen%C3%A7a-ISC-green?style=for-the-badge)

> **"O desenvolvimento deve ser avaliado pela expansão das liberdades humanas."** — *Amartya Sen*

> **Nota de Repositório:** O código-fonte da aplicação passou a ser mantido em **repositório privado** (`dhiogoFrutuoso/Portal-Voz-Ativa`). Este repositório público preserva o **README oficial**, o **documento de apresentação do projeto ([PORTAL_VOZ_ATIVA.pdf](./PORTAL_VOZ_ATIVA.pdf))** e a **árvore estrutural de diretórios** seguida pelo sistema, **sem exposição de código-fonte**.

---

## Sobre o Projeto

O **Portal Voz Ativa** é uma iniciativa cívica independente de **Tecnologia Social** voltada à cidade de **Cariús (CE)**, vencedora do **Ceará de Valores** com o **1º lugar estadual** e o **1º lugar regional de Iguatu** (premiação de **R$ 20.000,00** para desenvolvimento). Mais do que uma plataforma digital, o sistema estabelece um canal direto de participação cidadã, escuta ativa e transparência comunitária.

### Reconhecimento

| Conquista | Detalhe |
| :--- | :--- |
| 1º Lugar Estadual | Ceará de Valores 2025 |
| 1º Lugar Regional | Região de Iguatu |
| Premiação | R$ 20.000,00 |

---

## Fundamentação Filosófica e Social

A concepção do Portal Voz Ativa apoia-se em quatro pilares intelectuais:

- **Aristóteles:** A cidade existe para proporcionar uma vida boa aos seus habitantes.
- **Paulo Freire:** Educação e consciência política como ferramentas de transformação social.
- **Hannah Arendt:** A cidadania nasce da ação e da participação no espaço público.
- **Pierre Lévy:** Valorização da inteligência coletiva e do saber distribuído.

---

## Funcionalidades e Pilares do Sistema

O ecossistema do portal organiza-se em três eixos principais de atendimento ao cidadão, integrados a módulos transversais de segurança, governança e acessibilidade:

### 1. Cidadania — Gestão de Melhorias
- Registro de feedbacks e demandas urbanas com geolocalização.
- Acompanhamento por protocolo e linha do tempo de atendimento.
- Moderação prévia e histórico de interações entre cidadão e gestão.

### 2. Segurança — Denúncias Sigilosas
- Canal dedicado para relatos de ocorrências e crimes ambientais/queimadas com proteção de identidade (`isConfidential`) e controle estrito de visibilidade.
- Geração de comprovantes de protocolo e relatórios estruturados para encaminhamento.

### 3. Economia — Vitrine do Trabalhador
- Espaço gratuito para divulgação de mão de obra autônoma e serviços locais em Cariús, conectando prestadores e moradores sem intermediários.

### Pilares Transversais de Arquitetura e Governança
- **Design System e Acessibilidade (4 Modos):** Interface inspirada no padrão gov.br (DSGOV) com suporte completo a **Modo Claro Padrão**, **Alto Contraste Claro**, **Modo Escuro** e **Modo Escuro + Alto Contraste acoplados**.
- **Autenticação e Segurança:** Sessões persistidas em MongoDB com Passport.js, identidade por JWT (`HS256` com `tokenVersion` para revogação), OTP com hash HMAC-SHA-256 e limite de tentativas, `helmet`, `express-rate-limit` e proteção CSRF.
- **Mídia e Validação:** Sanitização e validação de uploads via `sharp` (conversão WebP/AVIF sem metadados EXIF), triagem de PDFs e entrega otimizada via Cloudinary.
- **Auditoria, Privacidade e SEO:** Registros imutáveis de auditoria administrativa e histórico de atividades (`AuditLog`, `ActivityLog`, `AccessLog`), banner de consentimento LGPD integrado ao Google Analytics 4 (Consent Mode v2), página `404` dedicada, `robots.txt` e `sitemap.xml`.

---

## Estrutura de Diretórios do Projeto

As pastas abaixo reproduzem exatamente a organização modular adotada pelo projeto (mantidas via `.gitkeep` sem arquivos de código):

```text
Portal-Voz-Ativa/
├── PORTAL_VOZ_ATIVA.pdf               # Documento de apresentação do projeto
├── README.md                          # Documentação geral e arquitetura
├── docs/                              # Guias de implantação (Vercel) e governança/segurança
├── scripts/                           # Scripts operacionais de migração, mídia e preparo de build
│   └── testes/                        # Suíte de testes de fluxos, views, reCAPTCHA, Vercel e governança
└── src/                               # Núcleo da aplicação web (padrão MVC em Node.js)
    ├── config/                        # Conexão MongoDB, autenticação, sessão, segurança e rate-limit
    ├── helpers/                       # Regras de validação, OTP, e-mail, mídia, auditoria, logs e RBAC
    ├── models/                        # Schemas Mongoose (usuários, categorias, denúncias, vitrine, mídia, OTP e logs)
    ├── public/                        # Ativos estáticos de origem (copiados para public/ no build da Vercel)
    │   ├── css/                       # Folhas de estilo globais e temas de acessibilidade
    │   ├── img/                       # Ilustrações e selos institucionais em WebP
    │   ├── js/                        # Scripts de upload seguro e interações do cliente
    │   └── pdf/                       # Material em PDF disponibilizado no portal
    ├── routes/                        # Controladores HTTP (público, categorias, contas, protocolos, uploads, legal e admin)
    └── views/                         # Templates Handlebars (SSR)
        ├── admin/                     # Painel administrativo, métricas, auditoria e relatórios
        ├── categories/                # Telas institucionais e fluxos específicos por eixo
        │   ├── denuncias_sigilosas/   # Abertura, hub e detalhes de denúncias
        │   ├── gestao_de_melhorias/   # Abertura, hub e detalhes de melhorias urbanas
        │   └── vitrine_do_trabalhador/# Cadastro, listagem e detalhes de prestadores
        ├── errors/                    # Página 404 personalizada
        ├── layouts/                   # Layout mestre compartilhado (navbar, consentimento LGPD, footer)
        ├── legal/                     # Termos de Uso e Política de Privacidade
        ├── partials/                  # Componentes reutilizáveis (cards, navbar, footer, mensagens e filtros)
        ├── project/                   # Páginas sobre o projeto e fundamentação
        ├── protocolos/                # Linha do tempo, listagem e comprovantes de protocolo
        └── users/                     # Cadastro, login, verificação OTP, recuperação de senha e perfil
```

---

## Stack Tecnológica

- **Runtime & Backend:** Node.js `24.x`, Express `5`, Express-Handlebars, Zod
- **Banco de Dados & Sessão:** MongoDB + Mongoose, `connect-mongo`, MongoDB Memory Server (testes)
- **Autenticação & Segurança:** Passport.js (`passport-local`), JWT (`HS256`), `bcryptjs`, `helmet`, `express-rate-limit`, Google reCAPTCHA v3
- **Mídia, Documentos & E-mail:** Multer, Sharp, Cloudinary, `pdf-lib`, Resend
- **Infraestrutura & Telemetria:** Vercel (Functions + CDN estática), Google Analytics 4 com Consent Mode v2 (LGPD)

---

## Resultados Esperados

| Confiança | Renda | Segurança |
| :--- | :--- | :--- |
| Histórico público e rastreável de sugestões e melhorias. | Novas frentes de trabalho para prestadores locais na Vitrine. | Canal sigiloso e ágil para relato de incidentes. |

---

## Equipe Técnica

**Responsável Geral:**
- **José Dhiogo Frutuoso Da Silva**

**Desenvolvedores:**
- Erik Mateus Vieira Carneiro
- Filipe Gomes do Nascimento
- Lawan Kelve Duarte Freitas
- Lucas Teixeira Gomes

---

## Acesso e Documentação

- **Portal Online:** [https://portal-voz-ativa.vercel.app](https://portal-voz-ativa.vercel.app)
- **PDF do Projeto:** [Visualizar PORTAL_VOZ_ATIVA.pdf](./PORTAL_VOZ_ATIVA.pdf)

---

<p align="center">
  Campeão Estadual do Ceará de Valores 2025 | Desenvolvido para a cidade de Cariús (CE).
</p>
