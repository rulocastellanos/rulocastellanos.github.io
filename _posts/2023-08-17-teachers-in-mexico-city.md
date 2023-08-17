---
title:  "Teachers in Mexico City by Sex and Municipality"
mathjax: true
layout: post
categories: media
---

![teachers_graph](https://github.com/rulocastellanos/rulocastellanos.github.io/assets/42686140/e52b6faf-8606-487b-bae7-8a9a016e5b36)

## Teachers related to early childhood education 

Most of the teacahers in Mexico City are female. Here I show teachers with positions related to early childhood education (43 days to 2 years) and preschool (3 to 5 years) grouped by gender.

## Code to do this graph 

Here I include the most important steps to obtain the graph. 

{% highlight c %}

#transform from long to wide 
data <- tidyr::pivot_longer(teachers, 
                            cols = c(docentes_mujeres, docentes_hombres), 
                            names_to = "sexo", values_to = "count")

#create graph 
graph <- ggplot(data, aes(x = reorder(municipio, count), y = count, fill = sexo)) +
  geom_bar(stat = "identity") +
  coord_flip() +
  scale_fill_manual(values = c("docentes_mujeres" = "#69b3a2", "docentes_hombres" = "#404080"),
                    labels = c("docentes_mujeres" = "Femenino", "docentes_hombres" = "Masculino")) +
  theme(plot.title = element_text(size = 20, face = "bold")) + 
  labs(title = "Docentes de la Ciudad de México\npor sexo y Alcaldía",
       x = "",
       y = "Total de docentes") 
                            

{% endhighlight %}


## Source 

[Ministry of Education of Mexico](https://www.planeacion.sep.gob.mx/principalescifras/) 
