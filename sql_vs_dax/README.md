
# 📚 Aprendendo DAX com SQL

## A primeira vista DAX parece um fórmula do Excel, mas vai dificultando conforme precisamos fazer análises mais avançadas

### Se você já conhece SQL, pode usar para facilitar a aprendizagem

### Desafios para treinar online:
- [Clientes sem Compras](../sql_vs_dax/clientes_sem_compras.txt) 
- [Retornando Clientes com mais de 5 Compras](../sql_vs_dax/clientes_com_mais_de_5_compras.txt)

### Cheet Sheet:

<img width="588" alt="image" src="https://github.com/marsolia/powerbi/assets/13143559/13d2a4f1-cad7-4fcd-a76d-5e52bccbcd36">

### Modelo Usado nos desafios
<img width="588" alt="image" src="https://github.com/marsolia/powerbi/assets/13143559/64a9f92b-1aa2-4cb7-a681-3ce672bfe1e6">



### Comparativas entre SQL vs DAX para ajudar no entendimento:


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

### ➡️ Comandos SQL com o equivalente DAX
<img width="588" alt="image" src="https://media.licdn.com/dms/image/D4D22AQF3WTXSmk8kiw/feedshare-shrink_800/0/1712834023894?e=1726704000&v=beta&t=Isu4G3R-QUohHdxT0ccWb7KyV01kVn0E-jUN8OH_dOk">


  

  


