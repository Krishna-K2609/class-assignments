    # Re-creating plot of canid ranges

    library("ggplot2")
    canids <- read.csv("/home/eeb177-student/Desktop/eeb177/homework/sorted-canid-ranges.csv", header = F, as.is = T)
    names(canids) <- c("genus", "species", "minage", "maxage")
    head(canids)

    ##       genus                 species   minage  maxage
    ## 1 Aelurodon      Aelurodon stirtoni 11.95000 14.7850
    ## 2 Aelurodon   Aelurodon montanensis  0.06885 14.7850
    ## 3 Aelurodon  Aelurodon wheelerianus 18.20000 25.6150
    ## 4 Aelurodon Aelurodon asthenostylus 14.78500 18.2000
    ## 5 Aelurodon      Aelurodon taxoides  7.60000 14.1815
    ## 6 Aelurodon         Aelurodon ferox  9.25000 14.7850

    canid_occ <- ggplot(canids, aes( species, ymin = maxage, ymax=minage, colour = genus))# plot data
    canid_occ <- canid_occ + geom_linerange() # draw ranges
    canid_occ <- canid_occ + theme(legend.position="none") # remove legend
    canid_occ <- canid_occ + coord_flip() # flip labels
    canid_occ <- canid_occ +  theme(axis.text.y = element_text(size=3)) # make species names smaller
    canid_occ <- canid_occ + theme(axis.ticks.y=element_blank()) # remove tick marks
    canid_occ <- canid_occ + scale_y_continuous(limits=c(0, 40), expand = c(0, 0), breaks=c(0, 10, 20, 30, 40)) # reduce empty space
    canid_occ <- canid_occ + labs(title = "Canid Fossil Occurrences", x = "Species", y = "Ma ago") + theme(plot.title = element_text(hjust = 0.5, size=22, face = "bold"), axis.title =element_text(size=20)) #adding title and modifying axes
    canid_occ

    ## Warning: Removed 5 rows containing missing values (geom_linerange).

![](classwork-Thursday-3-9_files/figure-markdown_strict/unnamed-chunk-1-1.png)

    ggsave(filename = "canid-occ.pdf", plot = canid_occ) # saving file in pdf format

    ## Saving 7 x 5 in image

    ## Warning: Removed 5 rows containing missing values (geom_linerange).

    # File is not sorted. Can use code that Mike will share to sort the data and make it more aesthetic. Or we can also use faceting.
