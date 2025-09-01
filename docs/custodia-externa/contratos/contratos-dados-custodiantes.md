# Catálogo de Contratos de Dados — Custodiantes Externos

## Custodiante ITAU

### **Arquivos/Feeds**

#### **Arquivo Principal: `posicoes_itau_diarias.csv`**

- **Frequência**: Diária (D+1)
- **Horário**: 06:00 GMT
- **Formato**: CSV com encoding UTF-8
- **Tamanho médio**: 100-300 MB
- **Compressão**: GZIP
- **Protocolo**: SFTP

#### **Arquivo de Ajustes: `ajustes_itau_intradiarios.csv`**

- **Frequência**: Sob demanda (máximo 5x por dia)
- **Horário**: 10:00, 12:00, 14:00, 16:00, 18:00 GMT
- **Formato**: CSV com encoding UTF-8
- **Tamanho médio**: 10-50 MB
- **Compressão**: GZIP

### **Campos e Tipos**

#### **Campos Obrigatórios:**

- **ISIN** (String, 12 caracteres): Identificador internacional do ativo
- **CODIGO_ITAU** (String, 15 caracteres): Código interno ITAU
- **CONTA** (String, 20 caracteres): Código da conta custodiada
- **DATA_POSICAO** (Date, DD/MM/AAAA): Data de referência da posição
- **QUANTIDADE** (Decimal, 18.6): Quantidade do ativo
- **PRECO_UNITARIO** (Decimal, 18.6): Preço unitário em moeda local
- **MOEDA_LOCAL** (String, 3 caracteres): Código ISO da moeda
- **VALOR_TOTAL** (Decimal, 18.2): Valor total da posição
- **TIPO_ATIVO** (String, 20 caracteres): Classificação do ativo

---

**📝 Documento gerado pelo agente data-architect-custody considerando padrões AMBIMA para contratos de dados de múltiplos custodiantes externos.**
