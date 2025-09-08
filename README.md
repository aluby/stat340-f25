# Stat340

This repo contains materials for the Fall 2025 iteration of Stat340: Bayesian Statistics at Carleton College. 

# R Code for generating hex sticker:

```{r}
library(tidyverse)
library(hexSticker)
library(showtext)

font_add_google("Patrick Hand", "patrick")

alpha_post <- 2 + 8
beta_post <- 3 + 10 - 8
like_scaled <- function(x) {
  like_fun <- function(x) {
    dbinom(x = 8, size = 10, prob = x)
  }
  scale_c <- integrate(like_fun, lower = 0, upper = 1)[[1]]
  like_fun(x)/scale_c
}

p <- ggplot(data = data.frame(x = c(0, 1)), aes(x)) +
  stat_function(fun = dbeta, args = list(shape1 = 2, shape2 = 3), geom = "line", alpha = .9, size = 3, aes(color = "prior")) +
  stat_function(fun = like_scaled, geom = "line", alpha = .9, size = 3,  aes(color = "(scaled) likelihood")) +
  theme_void() + 
  theme_transparent() +
  scale_color_manual(values = c("#fcfc62ff", "#e2583eff")) + 
  #scale_color_manual(values = NULL) + 
  theme(legend.position = "none")

sticker(p, package = "", p_size = 20, 
        url = "Stat340", u_x = .35, u_y = 1.35,  u_size = 20,
        h_size = 3, h_fill = "#FAE1DC", h_color = "#00ccccff",
        u_family = "patrick", u_color = "#00ccccff", 
        s_x = 1, s_y = .98, s_width = 1.4, s_height =1.3, filename = "images/bayes-logo.png")
```
