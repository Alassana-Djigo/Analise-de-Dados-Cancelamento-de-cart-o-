1)Importar as bases de dados
2)Visualizar e tratar as bases de dados
3)Analisar a base
	3.1)Linhas
	3.2)colunas
	3.3)Dados brutos
4)Construir uma analise para indetificar o problema

Nota1:Informações a falta não ajudam na analise, podem ser preechidas com uma media
ou se a coluna não for tão relevante na analise eliminar-lhe


Na Celula 9 outras maneiras de mostrar :
___________________________________________________________________________________________
"no CMD #pip install plotly"
import plotly.express as px

contagem_cancelamentos_por_categoria = tabela.groupby("Categoria")["Idade"].count().reset_index(name="Contagem")
grafico = px.bar(contagem_cancelamentos_por_categoria, x="Categoria", color="Categoria", y="Contagem", title="Contagem de Cancelamentos por Categoria")
grafico.show()

___________________________________________________________________________________________
"no CMD #pip install bokeh"

from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource

output_file("stacked_bar.html")

source = ColumnDataSource(data=tabela)

p = figure(x_range=tabela['Categoria'], plot_height=350, title="Contagem de Cancelamentos por Categoria",
           toolbar_location=None, tools="")

p.vbar_stack(["Idade"], x='Categoria', source=source, color=("red", "green"), width=0.9)

p.y_range.start = 0
p.x_range.range_padding = 0.1
p.xgrid.grid_line_color = None
p.axis.minor_tick_line_color = None
p.outline_line_color = None
p.legend.location = "top_right"
p.legend.orientation = "horizontal"

show(p)
___________________________________________________________________________________________
"no CMD #pip install seaborn"
import seaborn as sns
import matplotlib.pyplot as plt

sns.countplot(x="Categoria", hue="Idade", data=tabela)
plt.show()



