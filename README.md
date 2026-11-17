# ⚙️ Sistemas Operacionais — Escalonamento de Processos

Atividade da disciplina de **Sistemas Operacionais 1** na **Fatec Taquaritinga**, com a resolução completa de exercícios de **escalonamento de processos**: algoritmos **FIFO** e **Circular (Round Robin)**, inclusive com **operações de E/S**.

✅ **Resolução completa:** [`Resolucao_Escalonamento_de_Processos.docx`](Resolucao_Escalonamento_de_Processos.docx), com gráficos de Gantt e cálculos

---

## 1️⃣ Preemptivo × Não-preemptivo

| Não-preemptivo | Preemptivo |
|---|---|
| O processo só sai da CPU quando **termina** ou **se bloqueia** | O SO pode **interromper** o processo (fim da fatia de tempo ou prioridade maior) |
| Menos trocas de contexto, mas um processo longo pode **monopolizar a CPU** | Divide melhor a CPU e responde mais rápido, com mais trocas de contexto |
| Ex.: FIFO (FCFS), SJF | Ex.: Circular (Round Robin), prioridade preemptiva, SRTF |

## 2️⃣ Os SOs modernos são preemptivos?

**Sim.** Windows, Linux, macOS, Android e iOS usam interrupções de relógio para retomar o controle da CPU. Isso garante multitarefa real e impede que um programa travado congele o sistema. Sistemas antigos, como o Windows 3.x e o Mac OS clássico, usavam multitarefa **cooperativa**.

---

## 📐 Convenções usadas

- **Turnaround** = término − criação
- **Tempo de espera** = tempo na fila de prontos = turnaround − CPU − tempo em E/S
- **"Instante t"** = o que acontece no intervalo de t até t+1
- No Circular, quem **chega** no mesmo instante de uma preempção entra na fila **antes** do preemptado

---

## 3️⃣ Processos A, B e C

| Processo | Criação | CPU |
|:---:|:---:|:---:|
| A | 0 | 4 |
| B | 3 | 5 |
| C | 4 | 7 |

### FIFO

```
|     A     |      B       |         C          |
0           4              9                    16
```

| Processo | Espera | Turnaround |
|:---:|:---:|:---:|
| A | 0 | 4 |
| B | 1 | 6 |
| C | 5 | 12 |
| **Média** | **2** | **7,33** |

**Instante 7:** A terminado · B executando · C pronto

### Circular (fatia = 3 u.t.)

```
|   A    |   B    |A |   C    |  B  |     C     |
0        3        6  7        10    12          16
```

| Processo | Espera | Turnaround |
|:---:|:---:|:---:|
| A | 3 | 7 |
| B | 4 | 9 |
| C | 5 | 12 |
| **Média** | **4** | **9,33** |

**Instante 7:** A terminado · B pronto · C executando

---

## 4️⃣ Processos A, B, C e D

| Processo | Criação | CPU |
|:---:|:---:|:---:|
| A | 0 | 2 |
| B | 3 | 6 |
| C | 5 | 3 |
| D | 2 | 3 |

### FIFO

```
|  A  |   D    |        B        |   C    |
0     2        5                 11       14
```

| Processo | Espera | Turnaround |
|:---:|:---:|:---:|
| A | 0 | 2 |
| B | 2 | 8 |
| C | 6 | 9 |
| D | 0 | 3 |
| **Média** | **2** | **5,5** |

**Instante 6:** A e D terminados · B executando · C pronto

### Circular (fatia = 2 u.t.)

```
|  A  |  D  |  B  |D |  C  |  B  |C |  B  |
0     2     4     6  7     9     11 12    14
```

| Processo | Espera | Turnaround |
|:---:|:---:|:---:|
| A | 0 | 2 |
| B | 5 | 11 |
| C | 4 | 7 |
| D | 2 | 5 |
| **Média** | **2,75** | **6,25** |

**Instante 6:** A terminado · D executando · B e C prontos

### Circular (fatia = 2 u.t.) com E/S em C

C faz E/S a cada 2 u.t. de execução e fica **bloqueado por 3 u.t.**

```
|  A  |  D  |  B  |D |  C  |     B     |C |
0     2     4     6  7     9           13 14
```

| Processo | Espera | Turnaround |
|:---:|:---:|:---:|
| A | 0 | 2 |
| B | 4 | 10 |
| C | 3 | 9 |
| D | 2 | 5 |
| **Média** | **2,25** | **6,5** |

**Instante 10:** A e D terminados · B executando · **C bloqueado (E/S de 9 a 12)**

---

## ✔️ Como os resultados foram conferidos

Todos os gráficos e tempos foram calculados à mão e depois **conferidos com um simulador de escalonamento**, que reproduziu exatamente os mesmos resultados.

---

## 🎓 Informações acadêmicas

| | |
|---|---|
| **Instituição** | Fatec Taquaritinga |
| **Curso** | Análise e Desenvolvimento de Sistemas — 3º semestre |
| **Disciplina** | Sistemas Operacionais 1 |
| **Professora** | Gislaine Cristina da Conceição |
| **Ano** | 2026 |

## 👤 Autor

**Juan Gabriel Pereira Augusto**
GitHub: [@JuanGabrielPereiraAugusto](https://github.com/JuanGabrielPereiraAugusto)
