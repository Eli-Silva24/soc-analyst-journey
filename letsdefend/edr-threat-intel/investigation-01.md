# 🔍 Investigação 01 — Hash Malicioso e Execução Suspeita de Endpoint

**Plataforma:** LetsDefend  
**Módulos:** EDR + Threat Intelligence Feed  
**Data:** 30/03/2026

---

## 📋 Cenário

Durante prática nos módulos de EDR e Threat Intelligence do LetsDefend,
realizei uma investigação correlacionando um hash suspeito com atividade
em endpoints da rede simulada.

---

## 🔎 O que investiguei

### 1. Identificação via Log Management
- Filtrei logs de Proxy usando uma URL suspeita como critério
- Identifiquei IP de origem: `172.16.17.54`

### 2. Consulta ao Threat Intelligence Feed
- Pesquisei o hash `53d405e839e53d408f5` no Threat Intel
- Hash classificado como **malware** (score 4.0, fonte: Abuse.ch)
- Correlacionei o hash com o endpoint **EricProd** (IP: `172.16.17.22`)

### 3. Análise do Endpoint — Usuário Roberto
- Endpoint: `172.16.17.38`, usuário primário: **Roberto**
- No histórico de terminal, identifiquei comando suspeito:
```
  C:/Windows/System32/mshta.exe C:/Users/roberto/Desktop/Psl.hta
```
- `mshta.exe` executando arquivo `.hta` direto da área de trabalho
  é técnica comum em ataques de **phishing e execução de malware**

---

## 🧠 Conclusão

| Indicador | Detalhe |
|-----------|---------|
| IP suspeito | 172.16.17.54 |
| Hash malicioso | 53d405e839e53d408f5 |
| Endpoint comprometido | EricProd (172.16.17.22) |
| Técnica identificada | Execução via mshta.exe + arquivo .hta |
| Ação recomendada | Isolamento do endpoint + análise forense |

---

## 📸 Screenshots

![Log Management](../../screenshots/log-management.png)

> ⚠️ Adicionar prints do Threat Intel e EDR

---

## 📚 O que aprendi

- Como correlacionar um hash de Threat Intelligence com um endpoint real
- Como identificar execução suspeita via histórico de terminal no EDR
- `mshta.exe` + `.hta` é um vetor clássico de ataque — associado ao
  MITRE ATT&CK T1218.005 (Signed Binary Proxy Execution)
