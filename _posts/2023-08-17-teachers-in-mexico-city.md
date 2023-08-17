---
title:  "Teachers in Mexico City by Sex and Municipality"
mathjax: true
layout: post
categories: media
---

![teachers_graph](https://github.com/rulocastellanos/rulocastellanos.github.io/assets/42686140/e52b6faf-8606-487b-bae7-8a9a016e5b36)

## Teachers 

Most of the teacahers in Mexico City are female.

## Code to do this graph 

Embed code by putting `{{ "{% highlight language " }}%}` `{{ "{% endhighlight " }}%}` blocks around it. Adding the parameter `linenos` will show source lines besides the code.

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
