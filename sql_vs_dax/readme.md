
# 📚 Aprendendo DAX com SQL

## A primeira vista DAX parece um fórmula do Excel, mas vai dificultando conforme precisamos fazer análises mais avançadas

### Se você já conhece SQL, pode usar para facilitar a aprendizagem

Veja esses comparativos podem ajudar:

𝗦𝗲𝗹𝗲𝗰𝗶𝗼𝗻𝗮𝗿 𝗗𝗮𝗱𝗼𝘀:
- SQL
SELECT * FROM Clientes

- DAX
EVALUATE Clientes

𝗔𝗽𝗲𝗻𝗮𝘀 𝗮𝗹𝗴𝘂𝗻𝘀 𝗰𝗮𝗺𝗽𝗼𝘀 𝗱𝗮 𝘁𝗮𝗯𝗲𝗹𝗮:
- SQL
SELECT Nome, Sobrenome FROM Clientes

- DAX
EVALUATE SUMMARIZE(Clientes, Clientes[Nome], Clientes[Sobrenome])

𝗖𝗹𝗮𝘀𝘀𝗶𝗳𝗶𝗰𝗮𝗿:
- SQL
SELECT * FROM Clientes ORDER BY Nome

- DAX
EVALUATE Clientes ORDER BY Clientes[Nome]

𝗥𝗮𝗻𝗸𝗶𝗻𝗴:
- SQL
SELECT TOP 10 * FROM Clientes ORDER BY Total DESC

- DAX:
EVALUATE TOPN(10, Clientes, Clientes[Total])

𝗔𝗴𝗿𝘂𝗽𝗮𝗻𝗱𝗼/𝗦𝘂𝗺𝗮𝗿𝗶𝘇𝗮𝗻𝗱𝗼 𝗥𝗲𝘀𝘂𝗹𝘁𝗮𝗱𝗼𝘀
- SQL
SELECT Nome, SUM(Total) Total
FROM Clientes GROUP BY Nome

- DAX:
EVALUATE
SUMMARIZE(Clientes,
  Clientes[Nome],Clientes[Sobrenome],
  Total, SUM('Clientes'[Total])

Cheet Sheet:

<img width="588" alt="image" src="https://github.com/marsolia/powerbi/assets/13143559/13d2a4f1-cad7-4fcd-a76d-5e52bccbcd36">
