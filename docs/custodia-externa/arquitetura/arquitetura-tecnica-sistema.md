# Arquitetura Técnica — Sistema de Custódia Externa

## Visão Geral da Arquitetura

### **Arquitetura de Alto Nível**

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Custodiante   │    │   Custodiante   │    │   Custodiante   │    │   Custodiante   │
│     ITAU        │    │    Bradesco     │    │    Santander    │    │     Caixa       │
│   (SFTP/CSV)    │    │   (SFTP/CSV)    │    │   (REST/JSON)   │    │   (SFTP/XML)    │
└─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘
          │                      │                      │                      │
          └──────────────────────┼──────────────────────┼──────────────────────┘
                                 │                      │
                    ┌─────────────▼─────────────┐       │
                    │    Gateway de Entrada     │       │
                    │   (Load Balancer + SSL)   │       │
                    └─────────────┬─────────────┘       │
                                 │                      │
                    ┌─────────────▼─────────────┐       │
                    │   Sistema de Validação    │       │
                    │   (Format + Content)     │       │
                    └─────────────┬─────────────┘       │
                                 │                      │
                    ┌─────────────▼─────────────┐       │
                    │   Processamento ETL       │       │
                    │   (Staging → Curated)    │       │
                    └─────────────┬─────────────┘       │
                                 │                      │
                    ┌─────────────▼─────────────┐       │
                    │   Sistema de              │       │
                    │   Reconciliação          │       │
                    └─────────────┬─────────────┘       │
                                 │                      │
                    ┌─────────────▼─────────────┐       │
                    │   Banco de Dados          │       │
                    │   (Produção)              │       │
                    └─────────────┬─────────────┘       │
                                 │                      │
                    ┌─────────────▼─────────────┐       │
                    │   APIs e Dashboards       │       │
                    │   (Frontend + Relatórios) │       │
                    └───────────────────────────┘       │
                                                         │
                    ┌────────────────────────────────────┘
                    │
                    ┌─────────────▼─────────────┐
                    │   Sistema Interno de      │
                    │   Precificação           │
                    │   (API REST)             │
                    └───────────────────────────┘
```

## Componentes do Sistema

### **1. Gateway de Entrada**

- **Load Balancer**: Distribuição de carga entre instâncias
- **SSL Termination**: Gerenciamento de certificados
- **Rate Limiting**: Controle de taxa de requisições por custodiante
- **IP Whitelisting**: Restrição de acesso por IP por custodiante
- **Protocol Adapter**: Conversão de SFTP/SWIFT/REST para formato interno

### **2. Sistema de Validação**

- **Validador de Formato**: Verificação de estrutura de arquivos por custodiante
- **Validador de Conteúdo**: Verificação de regras de negócio conforme AMBIMA
- **Validador de Compliance**: Verificação de regras regulatórias BACEN/CVM/AMBIMA
- **Sistema de Quarentena**: Isolamento de arquivos com problemas por custodiante
- **Validador de Integridade**: Checksums e validação de dados

---

**📝 Documento gerado pelo arquiteto de sistemas considerando tecnologias e padrões para implementação do sistema de custódia externa com integração ao sistema interno de precificação.**
