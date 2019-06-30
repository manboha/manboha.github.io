---
title:  "[R] Basic Graphics with ggplot2"
tags:
  - R
  - ggplot2  
toc: true
toc_label: "ON THIS PAGE"
---

*source : Garrett Grolemund & Hadley Wickham, R for Data Science, 2017*

## Creating a ggplot graphic
```
library(ggplot2)

# displ on the x-axis and hwy on the y-axis
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
```

ggplot code template
```
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(
     mapping = aes(<MAPPINGS>),
     stat = <STAT>, 
     position = <POSITION>
  ) +
  <COORDINATE_FUNCTION> +
  <FACET_FUNCTION>
```

##  Aesthetic mappings
```
# mapped class to the color aesthetic
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
  
# mapped class to the size aesthetic
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, size = class))
  
# mapped class to the alpha aesthetic(transparency)
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
  
# mapped class to the shape aesthetic
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))  
```
```
#  make all of the points blue
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```
```
# mapped 'displ < 5' to the color aesthetic
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))
```

## Facets
```
# to facet plot by a single variable : facet_wrap()
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)

# to facet plot on the combination of two variables : facet_grid()
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_grid(drv ~ cyl)
```
```
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

## Geometric objects
```
# smooth line 
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy))

# three lines based on their drv value
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))

#  overlaying
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = drv)) ) +
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```
```
# categorical variable to draw multiple objects
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
    
ggplot(data = mpg) +
  geom_smooth(
    mapping = aes(x = displ, y = hwy, color = drv),
    show.legend = FALSE
  )
```
```
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth(data = filter(mpg, class == "subcompact"), se = FALSE)
```
```
# two graphs look the same
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()

ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

## Statistical transformations
```
# displays the total number of diamonds grouped by cut
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut))

# or
ggplot(data = diamonds) + 
  stat_count(mapping = aes(x = cut))
```

The default stat of geom_bar() is `count`.
Other value for stat are `identity`.
```
# displays the total number of diamonds grouped by cut
demo <- diamonds %>% group_by(cut) %>% summarise(freq = n())
ggplot(data = demo) +
  geom_bar(mapping = aes(x = cut, y = freq), stat = "identity")
```
```
# display a bar chart of proportion
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., group = 1))
```

## Position adjustments
```
# `colour` aesthetic
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, colour = cut))

# `fill` aesthetic
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = cut))
```
```
# combination of cut and clarity : default position = stack
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity))

# position = "identity" : overlap problem for bars
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + 
  geom_bar(alpha = 1/5, position = "identity")
ggplot(data = diamonds, mapping = aes(x = cut, colour = clarity)) + 
  geom_bar(fill = NA, position = "identity")

# position = "fill" : compare proportions across groups
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity), position = "fill")

# position = "dodge" : compare individual values
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity), position = "dodge")

# position = "jitter" : random noise to each point for overplotting problem
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), position = "jitter")
```
```
# overplotting problem
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
  
# geom_jitter() and the amount of jittering
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 0.5, height = 0.5)

# geom_count() : size of point
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_count()

```

## Coordinate systems
```
# coord_flip() switches the x and y axes
ggplot(data = mpg, mapping = aes(x = class, y = hwy)) + 
  geom_boxplot() +
  coord_flip()
```
```
# coord_quickmap() sets the aspect ratio correctly for maps
map <- map_data("nz")

ggplot(map, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black")

ggplot(map, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black") +
  coord_quickmap()

ggplot(map, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black") +
  coord_map()
```
```
# coord_polar() uses polar coordinates
bar <- ggplot(data = diamonds) + 
  geom_bar(
    mapping = aes(x = cut, fill = cut), 
    show.legend = FALSE,
    width = 1
  ) + 
  theme(aspect.ratio = 1) +
  labs(x = NULL, y = NULL)

bar + coord_flip()
bar + coord_polar()
```
```
# coord_fixed(): fixed "aspect ratio"(default: ratio=1)
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  geom_abline() + # default: intercept = 0, slope = 1
  coord_fixed()
```
