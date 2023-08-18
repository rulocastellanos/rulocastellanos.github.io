---
title:  "Elderly Care Homes in Mexico City"
mathjax: true
layout: post
categories: media
---

![asilos_map](https://github.com/rulocastellanos/rulocastellanos.github.io/assets/42686140/e2147839-b279-4a57-a5fe-e116f10a934f)

## Elderly Care Homes

According to [DENUE](https://www.inegi.org.mx/app/mapa/denue/), there are 20 establishments registered as "Elderly Care Homes and other public sector residences for the care of the elderly" in Mexico City. Out of the 16 Alcaldias (Municipalities) in the city, 12 have registered elderly care homes as per DENUE records. The Alcaldias with the highest number of such homes are Benito Juárez and Gustavo A. Madero, each having 3 care homes.

# Code to do this graph

{% highlight c %}

#read the data from DENUE
denue <- read_csv("data/inegi/denue_asilos/INEGI_DENUE_18082023.csv", 
                  locale = locale(encoding = "ISO-8859-1")) %>% 
  clean_names() %>% 
  filter(entidad_federativa == "CIUDAD DE MÉXICO") %>% 
  select("municipio", "nombre_de_clase_de_la_actividad","latitud", "longitud")

#read the shapefile of Mexico City's Municipalities 
alcaldias <-st_read("/Users/(...)/limite_de_las_alcaldias/limite_de_las_alcaldias.shp")

#Left join data after some homologation  
map_data <- left_join(alcaldias, denue, by = c("nomgeo" = "municipio"))

#create map 
asilos_map <- ggplot() +
  geom_sf(data = alcaldias) +  # Plot the polygon boundaries
  geom_point(data = denue %>% filter(!is.na(latitud) & !is.na(longitud)),
             aes(x = longitud, y = latitud),
             color = "#404080", size = 2) +  # Plot the points of asilos
  theme_minimal() +
  theme(plot.title = element_text(size = 20, face = "bold")) + 
  labs(title = "Casas de cuidado para adultos mayores en la Ciudad de México\n según el DENUE (2022)",
       x = "", y = "", caption = "Elaborado por Raul Castellanos con datos del DENUE")



{% endhighlight %}

# Source 

[Directorio Estadístico Nacional de Unidades Económicas (DENUE)](https://www.inegi.org.mx/app/mapa/denue/)


