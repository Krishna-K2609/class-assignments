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

    # Re-creating plot of canid ranges using the code done on Tuesday.
    library(paleotree)

    ## Loading required package: ape

    library(paleobioDB)

    ## Loading required package: raster

    ## Loading required package: sp

    ## 
    ## Attaching package: 'raster'

    ## The following objects are masked from 'package:ape':
    ## 
    ##     rotate, zoom

    ## Loading required package: maps

    # Download the data
    data(graptPBDB)
    head(graptOccPBDB)

    ##   occurrence_no record_type reid_no obsolete collection_no
    ## 1          1669  occurrence      NA       NA           215
    ## 2          2186  occurrence      NA       NA           256
    ## 3          2216  occurrence      NA       NA           258
    ## 4          2217  occurrence      NA       NA           258
    ## 5          2318  occurrence      NA       NA           270
    ## 6          2319  occurrence      NA       NA           270
    ##      identified_name identified_rank identified_no taxonomic_reason
    ## 1  Chaunograptus sp.           genus         33800                 
    ## 2  Dendrograptus sp.           genus         33551                 
    ## 3 Acanthograptus sp.           genus         33536                 
    ## 4  Dendrograptus sp.           genus         33551                 
    ## 5  Dendrograptus sp.           genus         33551                 
    ## 6   Hallograptus sp.           genus         33673                 
    ##    accepted_name accepted_rank accepted_no early_interval late_interval
    ## 1  Chaunograptus         genus       33800      St Davids     St Davids
    ## 2  Dendrograptus         genus       33551  Trempealeauan Trempealeauan
    ## 3 Acanthograptus         genus       33536       Cambrian      Cambrian
    ## 4  Dendrograptus         genus       33551       Cambrian      Cambrian
    ## 5  Dendrograptus         genus       33551       Tremadoc      Tremadoc
    ## 6   Hallograptus         genus       33673       Tremadoc      Tremadoc
    ##   early_age late_age reference_no   primary_name primary_reso
    ## 1     513.0    501.0           13  Chaunograptus             
    ## 2     501.0    485.4           13  Dendrograptus             
    ## 3     541.0    485.4           13 Acanthograptus             
    ## 4     541.0    485.4           13  Dendrograptus             
    ## 5     485.4    477.7           13  Dendrograptus             
    ## 6     485.4    477.7           13   Hallograptus             
    ##   subgenus_name subgenus_reso species_name species_reso subgenus
    ## 1                                      sp.                    NA
    ## 2                                      sp.                    NA
    ## 3                                      sp.                    NA
    ## 4                                      sp.                    NA
    ## 5                                      sp.                    NA
    ## 6                                      sp.                    NA
    ##   subgenus_no          genus genus_no family family_no        order
    ## 1          NA  Chaunograptus    33800               NA             
    ## 2          NA  Dendrograptus    33551               NA   Dendroidea
    ## 3          NA Acanthograptus    33536               NA   Dendroidea
    ## 4          NA  Dendrograptus    33551               NA   Dendroidea
    ## 5          NA  Dendrograptus    33551               NA   Dendroidea
    ## 6          NA   Hallograptus    33673               NA Graptoloidea
    ##   order_no         class class_no       phylum phylum_no   authorizer
    ## 1       NA Graptolithina    33534 Hemichordata     33518 Sepkoski, J.
    ## 2    33535 Graptolithina    33534 Hemichordata     33518 Sepkoski, J.
    ## 3    33535 Graptolithina    33534 Hemichordata     33518 Sepkoski, J.
    ## 4    33535 Graptolithina    33534 Hemichordata     33518 Sepkoski, J.
    ## 5    33535 Graptolithina    33534 Hemichordata     33518 Sepkoski, J.
    ## 6    33606 Graptolithina    33534 Hemichordata     33518 Sepkoski, J.
    ##       enterer modifier
    ## 1 Sommers, M.  unknown
    ## 2 Sommers, M.  unknown
    ## 3 Sommers, M.  unknown
    ## 4 Sommers, M.  unknown
    ## 5 Sommers, M.  unknown
    ## 6 Sommers, M.  unknown

    # Let's look at uncertainty for species and genera
    occSpecies <- taxonSortPBDBocc(graptOccPBDB, rank="species") # this sorts unique taxa and lists first and last occurrences
    head(occSpecies)

    ## $`Adelograptus antiquus`
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 3609        596430  occurrence      NA       NA         63189
    ## 3612        596434  occurrence      NA       NA         63190
    ## 3627        596451  occurrence      NA       NA         63192
    ## 3630        596454  occurrence      NA       NA         63194
    ## 3632        596458  occurrence      NA       NA         63195
    ## 3667        596498  occurrence      NA       NA         63204
    ## 4223        826761  occurrence      NA       NA         91172
    ##              identified_name identified_rank identified_no
    ## 3609 Adelograptus ? antiquus         species         84007
    ## 3612 Adelograptus ? antiquus         species         84007
    ## 3627 Adelograptus ? antiquus         species         84007
    ## 3630 Adelograptus ? antiquus         species         84007
    ## 3632 Adelograptus ? antiquus         species         84007
    ## 3667 Adelograptus ? antiquus         species         84007
    ## 4223   Adelograptus antiquus         species         84007
    ##      taxonomic_reason         accepted_name accepted_rank accepted_no
    ## 3609             <NA> Adelograptus antiquus       species       84007
    ## 3612             <NA> Adelograptus antiquus       species       84007
    ## 3627             <NA> Adelograptus antiquus       species       84007
    ## 3630             <NA> Adelograptus antiquus       species       84007
    ## 3632             <NA> Adelograptus antiquus       species       84007
    ## 3667             <NA> Adelograptus antiquus       species       84007
    ## 4223             <NA> Adelograptus antiquus       species       84007
    ##      early_interval late_interval early_age late_age reference_no
    ## 3609    Tremadocian   Tremadocian     485.4    477.7        18179
    ## 3612  Lancefieldian   Bendigonian     485.4    473.9        18179
    ## 3627  Lancefieldian   Bendigonian     485.4    473.9        18179
    ## 3630    Tremadocian   Tremadocian     485.4    477.7        18179
    ## 3632    Tremadocian   Tremadocian     485.4    477.7        18179
    ## 3667    Tremadocian   Tremadocian     485.4    477.7        18179
    ## 4223        Ibexian       Ibexian     488.3    471.8        24434
    ##      primary_name primary_reso subgenus_name subgenus_reso species_name
    ## 3609 Adelograptus            ?          <NA>          <NA>     antiquus
    ## 3612 Adelograptus            ?          <NA>          <NA>     antiquus
    ## 3627 Adelograptus            ?          <NA>          <NA>     antiquus
    ## 3630 Adelograptus            ?          <NA>          <NA>     antiquus
    ## 3632 Adelograptus            ?          <NA>          <NA>     antiquus
    ## 3667 Adelograptus            ?          <NA>          <NA>     antiquus
    ## 4223 Adelograptus         <NA>          <NA>          <NA>     antiquus
    ##      species_reso subgenus subgenus_no        genus genus_no family
    ## 3609         <NA>       NA          NA Adelograptus    33537   <NA>
    ## 3612         <NA>       NA          NA Adelograptus    33537   <NA>
    ## 3627         <NA>       NA          NA Adelograptus    33537   <NA>
    ## 3630         <NA>       NA          NA Adelograptus    33537   <NA>
    ## 3632         <NA>       NA          NA Adelograptus    33537   <NA>
    ## 3667         <NA>       NA          NA Adelograptus    33537   <NA>
    ## 4223         <NA>       NA          NA Adelograptus    33537   <NA>
    ##      family_no      order order_no         class class_no       phylum
    ## 3609        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3612        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3627        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3630        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3632        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3667        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 4223        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ##      phylum_no  authorizer     enterer  modifier
    ## 3609     33518   Hendy, A.   Hendy, A. Hendy, A.
    ## 3612     33518   Hendy, A.   Hendy, A.   unknown
    ## 3627     33518   Hendy, A.   Hendy, A.   unknown
    ## 3630     33518   Hendy, A.   Hendy, A. Hendy, A.
    ## 3632     33518   Hendy, A.   Hendy, A.   unknown
    ## 3667     33518   Hendy, A.   Hendy, A.   unknown
    ## 4223     33518 Villier, L. Villier, L.   unknown
    ## 
    ## $`Adelograptus clarki`
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 3610        596431  occurrence      NA       NA         63189
    ## 3633        596459  occurrence      NA       NA         63195
    ##          identified_name identified_rank identified_no taxonomic_reason
    ## 3610 Adelograptus clarki         species         84009             <NA>
    ## 3633 Adelograptus clarki         species         84009             <NA>
    ##            accepted_name accepted_rank accepted_no early_interval
    ## 3610 Adelograptus clarki       species       84009    Tremadocian
    ## 3633 Adelograptus clarki       species       84009    Tremadocian
    ##      late_interval early_age late_age reference_no primary_name
    ## 3610   Tremadocian     485.4    477.7        18179 Adelograptus
    ## 3633   Tremadocian     485.4    477.7        18179 Adelograptus
    ##      primary_reso subgenus_name subgenus_reso species_name species_reso
    ## 3610         <NA>          <NA>          <NA>       clarki         <NA>
    ## 3633         <NA>          <NA>          <NA>       clarki         <NA>
    ##      subgenus subgenus_no        genus genus_no family family_no
    ## 3610       NA          NA Adelograptus    33537   <NA>        NA
    ## 3633       NA          NA Adelograptus    33537   <NA>        NA
    ##           order order_no         class class_no       phylum phylum_no
    ## 3610 Dendroidea    33535 Graptolithina    33534 Hemichordata     33518
    ## 3633 Dendroidea    33535 Graptolithina    33534 Hemichordata     33518
    ##      authorizer   enterer  modifier
    ## 3610  Hendy, A. Hendy, A. Hendy, A.
    ## 3633  Hendy, A. Hendy, A.   unknown
    ## 
    ## $`Amplexograptus rugosus`
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 5893       1256955  occurrence      NA       NA        166800
    ##             identified_name identified_rank identified_no taxonomic_reason
    ## 5893 Amplexograptus rugosus         species        315895             <NA>
    ##               accepted_name accepted_rank accepted_no early_interval
    ## 5893 Amplexograptus rugosus       species      315895    Longvillian
    ##      late_interval early_age late_age reference_no   primary_name
    ## 5893 Marshbrookian     457.5      452          102 Amplexograptus
    ##      primary_reso subgenus_name subgenus_reso species_name species_reso
    ## 5893         <NA>          <NA>          <NA>      rugosus         <NA>
    ##      subgenus subgenus_no          genus genus_no family family_no
    ## 5893       NA          NA Amplexograptus    33615   <NA>        NA
    ##             order order_no         class class_no       phylum phylum_no
    ## 5893 Graptoloidea    33606 Graptolithina    33534 Hemichordata     33518
    ##      authorizer    enterer modifier
    ## 5893 Wagner, P. Wagner, P.  unknown
    ## 
    ## $`Azygograptus novozealandicus`
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 3898        601800  occurrence      NA       NA         63967
    ## 3960        601885  occurrence      NA       NA         63960
    ## 3964        601889  occurrence      NA       NA         63961
    ## 3993        601921  occurrence      NA       NA         63963
    ## 4014        601945  occurrence      NA       NA         63965
    ##                          identified_name identified_rank identified_no
    ## 3898        Azygograptus novozealandicus         species         84630
    ## 3960        Azygograptus novozealandicus         species         84630
    ## 3964        Azygograptus novozealandicus         species         84630
    ## 3993 Azygograptus novozealandicus n. sp.         species         84630
    ## 4014        Azygograptus novozealandicus         species         84630
    ##      taxonomic_reason                accepted_name accepted_rank
    ## 3898             <NA> Azygograptus novozealandicus       species
    ## 3960             <NA> Azygograptus novozealandicus       species
    ## 3964             <NA> Azygograptus novozealandicus       species
    ## 3993             <NA> Azygograptus novozealandicus       species
    ## 4014             <NA> Azygograptus novozealandicus       species
    ##      accepted_no early_interval late_interval early_age late_age
    ## 3898       84630     Gisbornian    Gisbornian     460.9    456.1
    ## 3960       84630     Gisbornian    Gisbornian     460.9    456.1
    ## 3964       84630     Gisbornian    Gisbornian     460.9    456.1
    ## 3993       84630    Darriwilian   Darriwilian     467.3    458.4
    ## 4014       84630     Gisbornian    Gisbornian     460.9    456.1
    ##      reference_no primary_name primary_reso subgenus_name subgenus_reso
    ## 3898        18428 Azygograptus         <NA>          <NA>          <NA>
    ## 3960        18428 Azygograptus         <NA>          <NA>          <NA>
    ## 3964        18428 Azygograptus         <NA>          <NA>          <NA>
    ## 3993        18428 Azygograptus         <NA>          <NA>          <NA>
    ## 4014        18428 Azygograptus         <NA>          <NA>          <NA>
    ##         species_name species_reso subgenus subgenus_no        genus
    ## 3898 novozealandicus         <NA>       NA          NA Azygograptus
    ## 3960 novozealandicus         <NA>       NA          NA Azygograptus
    ## 3964 novozealandicus         <NA>       NA          NA Azygograptus
    ## 3993 novozealandicus       n. sp.       NA          NA Azygograptus
    ## 4014 novozealandicus         <NA>       NA          NA Azygograptus
    ##      genus_no family family_no        order order_no         class
    ## 3898    33628   <NA>        NA Graptoloidea    33606 Graptolithina
    ## 3960    33628   <NA>        NA Graptoloidea    33606 Graptolithina
    ## 3964    33628   <NA>        NA Graptoloidea    33606 Graptolithina
    ## 3993    33628   <NA>        NA Graptoloidea    33606 Graptolithina
    ## 4014    33628   <NA>        NA Graptoloidea    33606 Graptolithina
    ##      class_no       phylum phylum_no authorizer   enterer modifier
    ## 3898    33534 Hemichordata     33518  Hendy, A. Hendy, A.  unknown
    ## 3960    33534 Hemichordata     33518  Hendy, A. Hendy, A.  unknown
    ## 3964    33534 Hemichordata     33518  Hendy, A. Hendy, A.  unknown
    ## 3993    33534 Hemichordata     33518  Hendy, A. Hendy, A.  unknown
    ## 4014    33534 Hemichordata     33518  Hendy, A. Hendy, A.  unknown
    ## 
    ## $`Climacograptus bicornis`
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 2399        246238  occurrence      NA       NA         24117
    ## 4166        748935  occurrence      NA       NA         80104
    ## 4320        955088  occurrence      NA       NA        111711
    ## 4325        955095  occurrence      NA       NA        111713
    ## 4332        955103  occurrence      NA       NA        111718
    ## 4516        996584  occurrence      NA       NA        120528
    ## 4685       1139721  occurrence      NA       NA        145233
    ## 4695       1139731  occurrence      NA       NA        145236
    ## 4703       1139741  occurrence      NA       NA        145237
    ## 4713       1139751  occurrence      NA       NA        145238
    ## 4725       1139763  occurrence      NA       NA        145240
    ## 4773       1141828  occurrence      NA       NA        145463
    ## 4774       1141829  occurrence      NA       NA        145464
    ## 5330       1144012  occurrence      NA       NA        145615
    ##              identified_name identified_rank identified_no
    ## 2399 Climacograptus bicornis         species        306375
    ## 4166 Climacograptus bicornis         species        306375
    ## 4320 Climacograptus bicornis         species        306375
    ## 4325 Climacograptus bicornis         species        306375
    ## 4332 Climacograptus bicornis         species        306375
    ## 4516 Climacograptus bicornis         species        306375
    ## 4685 Climacograptus bicornis         species        306375
    ## 4695 Climacograptus bicornis         species        306375
    ## 4703 Climacograptus bicornis         species        306375
    ## 4713 Climacograptus bicornis         species        306375
    ## 4725 Climacograptus bicornis         species        306375
    ## 4773 Climacograptus bicornis         species        306375
    ## 4774 Climacograptus bicornis         species        306375
    ## 5330 Climacograptus bicornis         species        306375
    ##      taxonomic_reason           accepted_name accepted_rank accepted_no
    ## 2399             <NA> Climacograptus bicornis       species      306375
    ## 4166             <NA> Climacograptus bicornis       species      306375
    ## 4320             <NA> Climacograptus bicornis       species      306375
    ## 4325             <NA> Climacograptus bicornis       species      306375
    ## 4332             <NA> Climacograptus bicornis       species      306375
    ## 4516             <NA> Climacograptus bicornis       species      306375
    ## 4685             <NA> Climacograptus bicornis       species      306375
    ## 4695             <NA> Climacograptus bicornis       species      306375
    ## 4703             <NA> Climacograptus bicornis       species      306375
    ## 4713             <NA> Climacograptus bicornis       species      306375
    ## 4725             <NA> Climacograptus bicornis       species      306375
    ## 4773             <NA> Climacograptus bicornis       species      306375
    ## 4774             <NA> Climacograptus bicornis       species      306375
    ## 5330             <NA> Climacograptus bicornis       species      306375
    ##       early_interval   late_interval early_age late_age reference_no
    ## 2399      Trentonian     Richmondian     460.9    443.7         6817
    ## 4166         Idavere         Idavere     460.9    455.8        26936
    ## 4320 Late Ordovician Late Ordovician     458.4    443.4        36540
    ## 4325 Late Ordovician Late Ordovician     458.4    443.4        36540
    ## 4332 Late Ordovician Late Ordovician     458.4    443.4        36540
    ## 4516        Sandbian        Sandbian     458.4    453.0        38521
    ## 4685      Gisbornian      Gisbornian     460.9    456.1        46966
    ## 4695      Gisbornian      Gisbornian     460.9    456.1        46966
    ## 4703      Gisbornian      Gisbornian     460.9    456.1        46966
    ## 4713      Gisbornian      Gisbornian     460.9    456.1        46966
    ## 4725      Gisbornian      Gisbornian     460.9    456.1        46966
    ## 4773       Eastonian       Eastonian     456.1    449.5        46966
    ## 4774       Eastonian       Eastonian     456.1    449.5        46966
    ## 5330      Caradocian      Caradocian     460.9    449.5        47089
    ##        primary_name primary_reso subgenus_name subgenus_reso species_name
    ## 2399 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4166 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4320 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4325 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4332 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4516 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4685 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4695 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4703 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4713 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4725 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4773 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 4774 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ## 5330 Climacograptus         <NA>          <NA>          <NA>     bicornis
    ##      species_reso subgenus subgenus_no          genus genus_no
    ## 2399         <NA>       NA          NA Climacograptus    33636
    ## 4166         <NA>       NA          NA Climacograptus    33636
    ## 4320         <NA>       NA          NA Climacograptus    33636
    ## 4325         <NA>       NA          NA Climacograptus    33636
    ## 4332         <NA>       NA          NA Climacograptus    33636
    ## 4516         <NA>       NA          NA Climacograptus    33636
    ## 4685         <NA>       NA          NA Climacograptus    33636
    ## 4695         <NA>       NA          NA Climacograptus    33636
    ## 4703         <NA>       NA          NA Climacograptus    33636
    ## 4713         <NA>       NA          NA Climacograptus    33636
    ## 4725         <NA>       NA          NA Climacograptus    33636
    ## 4773         <NA>       NA          NA Climacograptus    33636
    ## 4774         <NA>       NA          NA Climacograptus    33636
    ## 5330         <NA>       NA          NA Climacograptus    33636
    ##              family family_no        order order_no         class class_no
    ## 2399 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4166 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4320 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4325 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4332 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4516 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4685 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4695 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4703 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4713 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4725 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4773 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 4774 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5330 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ##            phylum phylum_no           authorizer    enterer   modifier
    ## 2399 Hemichordata     33518          Holland, S. Hanson, T.    unknown
    ## 4166 Hemichordata     33518 Novack-Gottshall, P.  Hearn, P. Wagner, P.
    ## 4320 Hemichordata     33518           Miller, A.  Kolbe, S.  Kolbe, S.
    ## 4325 Hemichordata     33518           Miller, A.  Kolbe, S.    unknown
    ## 4332 Hemichordata     33518           Miller, A.  Kolbe, S.    unknown
    ## 4516 Hemichordata     33518        Kiessling, W. Merkel, U.    unknown
    ## 4685 Hemichordata     33518        Kiessling, W. Krause, M.    unknown
    ## 4695 Hemichordata     33518        Kiessling, W. Krause, M. Krause, M.
    ## 4703 Hemichordata     33518        Kiessling, W. Krause, M.    unknown
    ## 4713 Hemichordata     33518        Kiessling, W. Krause, M.    unknown
    ## 4725 Hemichordata     33518        Kiessling, W. Krause, M.    unknown
    ## 4773 Hemichordata     33518        Kiessling, W. Krause, M. Krause, M.
    ## 4774 Hemichordata     33518        Kiessling, W. Krause, M. Krause, M.
    ## 5330 Hemichordata     33518        Kiessling, W. Krause, M.    unknown
    ## 
    ## $`Climacograptus scalaris`
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 233          41894  occurrence      NA       NA          3281
    ## 236          41899  occurrence      NA       NA          3282
    ## 2530        260374  occurrence      NA       NA         25168
    ## 2884        285928  occurrence      NA       NA         27197
    ## 2948        287240  occurrence      NA       NA         27388
    ## 3173        291182  occurrence      NA       NA         27782
    ## 3246        292390  occurrence      NA       NA         27838
    ## 5115       1143763  occurrence      NA       NA        145587
    ## 5122       1143780  occurrence      NA       NA        145589
    ## 5132       1143790  occurrence      NA       NA        145590
    ## 5154       1143812  occurrence      NA       NA        145591
    ## 5204       1143865  occurrence      NA       NA        145598
    ## 5344       1144116  occurrence      NA       NA        145653
    ## 5355       1144128  occurrence      NA       NA        145654
    ## 5365       1144142  occurrence      NA       NA        145655
    ## 5385       1144162  occurrence      NA       NA        145656
    ## 5871       1218886  occurrence      NA       NA        159343
    ## 5896       1257991  occurrence      NA       NA        166909
    ##                identified_name identified_rank identified_no
    ## 233    Climacograptus scalaris         species        316364
    ## 236    Climacograptus scalaris         species        316364
    ## 2530   Climacograptus scalaris         species        316364
    ## 2884   Climacograptus scalaris         species        316364
    ## 2948   Climacograptus scalaris         species        316364
    ## 3173   Climacograptus scalaris         species        316364
    ## 3246   Climacograptus scalaris         species        316364
    ## 5115   Climacograptus scalaris         species        316364
    ## 5122 Climacograptus ? scalaris         species        316364
    ## 5132   Climacograptus scalaris         species        316364
    ## 5154   Climacograptus scalaris         species        316364
    ## 5204   Climacograptus scalaris         species        316364
    ## 5344   Climacograptus scalaris         species        316364
    ## 5355   Climacograptus scalaris         species        316364
    ## 5365   Climacograptus scalaris         species        316364
    ## 5385   Climacograptus scalaris         species        316364
    ## 5871   Climacograptus scalaris         species        316364
    ## 5896   Climacograptus scalaris         species        316364
    ##      taxonomic_reason           accepted_name accepted_rank accepted_no
    ## 233              <NA> Climacograptus scalaris       species      316364
    ## 236              <NA> Climacograptus scalaris       species      316364
    ## 2530             <NA> Climacograptus scalaris       species      316364
    ## 2884             <NA> Climacograptus scalaris       species      316364
    ## 2948             <NA> Climacograptus scalaris       species      316364
    ## 3173             <NA> Climacograptus scalaris       species      316364
    ## 3246             <NA> Climacograptus scalaris       species      316364
    ## 5115             <NA> Climacograptus scalaris       species      316364
    ## 5122             <NA> Climacograptus scalaris       species      316364
    ## 5132             <NA> Climacograptus scalaris       species      316364
    ## 5154             <NA> Climacograptus scalaris       species      316364
    ## 5204             <NA> Climacograptus scalaris       species      316364
    ## 5344             <NA> Climacograptus scalaris       species      316364
    ## 5355             <NA> Climacograptus scalaris       species      316364
    ## 5365             <NA> Climacograptus scalaris       species      316364
    ## 5385             <NA> Climacograptus scalaris       species      316364
    ## 5871             <NA> Climacograptus scalaris       species      316364
    ## 5896             <NA> Climacograptus scalaris       species      316364
    ##      early_interval late_interval early_age late_age reference_no
    ## 233        Aeronian      Aeronian     440.8    438.5          155
    ## 236        Aeronian      Aeronian     440.8    438.5          155
    ## 2530    Alexandrian   Alexandrian     443.4    436.0         7063
    ## 2884     Llandovery    Llandovery     443.4    433.4         7455
    ## 2948     Rhuddanian    Rhuddanian     443.4    440.8         7455
    ## 3173     Llandovery    Llandovery     443.4    433.4         7624
    ## 3246     Llandovery    Llandovery     443.4    433.4         7624
    ## 5115     Llandovery    Llandovery     443.4    433.4        47076
    ## 5122     Llandovery    Llandovery     443.4    433.4        47076
    ## 5132     Llandovery    Llandovery     443.4    433.4        47076
    ## 5154     Llandovery    Llandovery     443.4    433.4        47076
    ## 5204     Llandovery    Llandovery     443.4    433.4        47083
    ## 5344     Rhuddanian    Rhuddanian     443.4    440.8        47103
    ## 5355     Rhuddanian    Rhuddanian     443.4    440.8        47103
    ## 5365       Aeronian      Aeronian     440.8    438.5        47103
    ## 5385       Aeronian      Aeronian     440.8    438.5        47103
    ## 5871       Aeronian      Aeronian     440.8    438.5        52096
    ## 5896      Bolindian     Bolindian     449.5    443.7           78
    ##        primary_name primary_reso subgenus_name subgenus_reso species_name
    ## 233  Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 236  Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 2530 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 2884 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 2948 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 3173 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 3246 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5115 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5122 Climacograptus            ?          <NA>          <NA>     scalaris
    ## 5132 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5154 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5204 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5344 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5355 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5365 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5385 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5871 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ## 5896 Climacograptus         <NA>          <NA>          <NA>     scalaris
    ##      species_reso subgenus subgenus_no          genus genus_no
    ## 233          <NA>       NA          NA Climacograptus    33636
    ## 236          <NA>       NA          NA Climacograptus    33636
    ## 2530         <NA>       NA          NA Climacograptus    33636
    ## 2884         <NA>       NA          NA Climacograptus    33636
    ## 2948         <NA>       NA          NA Climacograptus    33636
    ## 3173         <NA>       NA          NA Climacograptus    33636
    ## 3246         <NA>       NA          NA Climacograptus    33636
    ## 5115         <NA>       NA          NA Climacograptus    33636
    ## 5122         <NA>       NA          NA Climacograptus    33636
    ## 5132         <NA>       NA          NA Climacograptus    33636
    ## 5154         <NA>       NA          NA Climacograptus    33636
    ## 5204         <NA>       NA          NA Climacograptus    33636
    ## 5344         <NA>       NA          NA Climacograptus    33636
    ## 5355         <NA>       NA          NA Climacograptus    33636
    ## 5365         <NA>       NA          NA Climacograptus    33636
    ## 5385         <NA>       NA          NA Climacograptus    33636
    ## 5871         <NA>       NA          NA Climacograptus    33636
    ## 5896         <NA>       NA          NA Climacograptus    33636
    ##              family family_no        order order_no         class class_no
    ## 233  Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 236  Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 2530 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 2884 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 2948 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 3173 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 3246 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5115 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5122 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5132 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5154 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5204 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5344 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5355 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5365 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5385 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5871 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ## 5896 Diplograptidae    150197 Graptoloidea    33606 Graptolithina    33534
    ##            phylum phylum_no    authorizer     enterer   modifier
    ## 233  Hemichordata     33518     Alroy, J. Sommers, M.    unknown
    ## 236  Hemichordata     33518     Alroy, J. Sommers, M.    unknown
    ## 2530 Hemichordata     33518   Holland, S.  Hanson, T.    unknown
    ## 2884 Hemichordata     33518     Foote, M.   Foote, M.    unknown
    ## 2948 Hemichordata     33518     Foote, M.   Foote, M.    unknown
    ## 3173 Hemichordata     33518     Foote, M.   Foote, M.    unknown
    ## 3246 Hemichordata     33518     Foote, M.   Foote, M.    unknown
    ## 5115 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5122 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5132 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5154 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5204 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5344 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5355 Hemichordata     33518 Kiessling, W.  Krause, M.    unknown
    ## 5365 Hemichordata     33518 Kiessling, W.  Krause, M. Krause, M.
    ## 5385 Hemichordata     33518 Kiessling, W.  Krause, M. Krause, M.
    ## 5871 Hemichordata     33518    Kroger, B.  Kroger, B.    unknown
    ## 5896 Hemichordata     33518    Wagner, P.  Wagner, P.    unknown

    occGenera <- taxonSortPBDBocc(graptOccPBDB, rank = "genus") # same for genera
    head(occGenera)

    ## $Abiesgraptus
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 5091       1143551  occurrence      NA       NA        145555
    ##       identified_name identified_rank identified_no taxonomic_reason
    ## 5091 Abiesgraptus sp.           genus         33607             <NA>
    ##      accepted_name accepted_rank accepted_no early_interval late_interval
    ## 5091  Abiesgraptus         genus       33607     Lochkovian    Lochkovian
    ##      early_age late_age reference_no primary_name primary_reso
    ## 5091     419.2    410.8        47062 Abiesgraptus         <NA>
    ##      subgenus_name subgenus_reso species_name species_reso subgenus
    ## 5091          <NA>          <NA>          sp.         <NA>       NA
    ##      subgenus_no        genus genus_no family family_no        order
    ## 5091          NA Abiesgraptus    33607   <NA>        NA Graptoloidea
    ##      order_no         class class_no       phylum phylum_no    authorizer
    ## 5091    33606 Graptolithina    33534 Hemichordata     33518 Kiessling, W.
    ##         enterer modifier
    ## 5091 Krause, M.  unknown
    ## 
    ## $Abrograptus
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 282          48923  occurrence      NA       NA          2933
    ## 1058        108139  occurrence      NA       NA          7761
    ## 1089        108245  occurrence      NA       NA          7770
    ##      identified_name identified_rank identified_no taxonomic_reason
    ## 282  Abrograptus sp.           genus         33608             <NA>
    ## 1058 Abrograptus sp.           genus         33608             <NA>
    ## 1089 Abrograptus sp.           genus         33608             <NA>
    ##      accepted_name accepted_rank accepted_no early_interval late_interval
    ## 282    Abrograptus         genus       33608  Late Llanvirn Late Llanvirn
    ## 1058   Abrograptus         genus       33608      Llandeilo     Llandeilo
    ## 1089   Abrograptus         genus       33608      Llandeilo     Llandeilo
    ##      early_age late_age reference_no primary_name primary_reso
    ## 282      463.5    460.9          104  Abrograptus         <NA>
    ## 1058     466.0    449.5          479  Abrograptus         <NA>
    ## 1089     466.0    449.5          480  Abrograptus         <NA>
    ##      subgenus_name subgenus_reso species_name species_reso subgenus
    ## 282           <NA>          <NA>          sp.         <NA>       NA
    ## 1058          <NA>          <NA>          sp.         <NA>       NA
    ## 1089          <NA>          <NA>          sp.         <NA>       NA
    ##      subgenus_no       genus genus_no family family_no        order
    ## 282           NA Abrograptus    33608   <NA>        NA Graptoloidea
    ## 1058          NA Abrograptus    33608   <NA>        NA Graptoloidea
    ## 1089          NA Abrograptus    33608   <NA>        NA Graptoloidea
    ##      order_no         class class_no       phylum phylum_no authorizer
    ## 282     33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 1058    33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 1089    33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ##                   enterer modifier
    ## 282  Novack-Gottshall, P.  unknown
    ## 1058 Novack-Gottshall, P.  unknown
    ## 1089 Novack-Gottshall, P.  unknown
    ## 
    ## $Acanthograptus
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 3             2216  occurrence      NA       NA           258
    ## 613         106163  occurrence      NA       NA          4724
    ## 614         106248  occurrence      NA       NA          4728
    ## 658         106590  occurrence      NA       NA          4770
    ## 851         107451  occurrence      NA       NA          7664
    ## 955         107809  occurrence      NA       NA          7719
    ## 975         107878  occurrence      NA       NA          7727
    ## 984         107912  occurrence      NA       NA          7728
    ## 988         107959  occurrence      NA       NA          7734
    ## 1049        108107  occurrence      NA       NA          7758
    ## 1245        108565  occurrence      NA       NA          7831
    ## 1358        118492  occurrence      NA       NA          8858
    ## 1518        140481  occurrence      NA       NA         12068
    ## 1792        156496  occurrence      NA       NA         13895
    ## 2019        160349  occurrence      NA       NA         14118
    ## 2085        240058  occurrence      NA       NA          7958
    ## 2098        240367  occurrence      NA       NA          7985
    ## 3336        292746  occurrence      NA       NA         27873
    ## 3395        293135  occurrence      NA       NA         27915
    ## 3408        380417  occurrence      NA       NA         36012
    ## 5847       1190922  occurrence      NA       NA         61727
    ## 5852       1196788  occurrence      NA       NA        154776
    ##                   identified_name identified_rank identified_no
    ## 3              Acanthograptus sp.           genus         33536
    ## 613            Acanthograptus sp.           genus         33536
    ## 614            Acanthograptus sp.           genus         33536
    ## 658            Acanthograptus sp.           genus         33536
    ## 851            Acanthograptus sp.           genus         33536
    ## 955            Acanthograptus sp.           genus         33536
    ## 975            Acanthograptus sp.           genus         33536
    ## 984            Acanthograptus sp.           genus         33536
    ## 988            Acanthograptus sp.           genus         33536
    ## 1049           Acanthograptus sp.           genus         33536
    ## 1245           Acanthograptus sp.           genus         33536
    ## 1358           Acanthograptus sp.           genus         33536
    ## 1518 Acanthograptus lejskoviensis         species         33536
    ## 1792           Acanthograptus sp.           genus         33536
    ## 2019           Acanthograptus sp.           genus         33536
    ## 2085           Acanthograptus sp.           genus         33536
    ## 2098           Acanthograptus sp.           genus         33536
    ## 3336           Acanthograptus sp.           genus         33536
    ## 3395           Acanthograptus sp.           genus         33536
    ## 3408           Acanthograptus sp.           genus         33536
    ## 5847           Acanthograptus sp.           genus         33536
    ## 5852           Acanthograptus sp.           genus         33536
    ##             taxonomic_reason  accepted_name accepted_rank accepted_no
    ## 3                       <NA> Acanthograptus         genus       33536
    ## 613                     <NA> Acanthograptus         genus       33536
    ## 614                     <NA> Acanthograptus         genus       33536
    ## 658                     <NA> Acanthograptus         genus       33536
    ## 851                     <NA> Acanthograptus         genus       33536
    ## 955                     <NA> Acanthograptus         genus       33536
    ## 975                     <NA> Acanthograptus         genus       33536
    ## 984                     <NA> Acanthograptus         genus       33536
    ## 988                     <NA> Acanthograptus         genus       33536
    ## 1049                    <NA> Acanthograptus         genus       33536
    ## 1245                    <NA> Acanthograptus         genus       33536
    ## 1358                    <NA> Acanthograptus         genus       33536
    ## 1518 taxon not fully entered Acanthograptus         genus       33536
    ## 1792                    <NA> Acanthograptus         genus       33536
    ## 2019                    <NA> Acanthograptus         genus       33536
    ## 2085                    <NA> Acanthograptus         genus       33536
    ## 2098                    <NA> Acanthograptus         genus       33536
    ## 3336                    <NA> Acanthograptus         genus       33536
    ## 3395                    <NA> Acanthograptus         genus       33536
    ## 3408                    <NA> Acanthograptus         genus       33536
    ## 5847                    <NA> Acanthograptus         genus       33536
    ## 5852                    <NA> Acanthograptus         genus       33536
    ##      early_interval late_interval early_age late_age reference_no
    ## 3          Cambrian      Cambrian     541.0    485.4           13
    ## 613          Arenig        Arenig     478.6    466.0          287
    ## 614        Tremadoc      Tremadoc     485.4    477.7          287
    ## 658        Tremadoc      Tremadoc     485.4    477.7          288
    ## 851        Tremadoc      Tremadoc     485.4    477.7          485
    ## 955        Tremadoc      Tremadoc     485.4    477.7          477
    ## 975           Dawan         Dawan     478.6    468.1          477
    ## 984        Tremadoc      Tremadoc     485.4    477.7          477
    ## 988          Arenig        Arenig     478.6    466.0          478
    ## 1049       Tremadoc      Tremadoc     485.4    477.7          479
    ## 1245       Tremadoc      Tremadoc     485.4    477.7          481
    ## 1358      Costonian   Longvillian     460.9    455.8          631
    ## 1518     Lochkovian    Lochkovian     419.2    410.8         4216
    ## 1792     Lochkovian    Lochkovian     419.2    410.8         6165
    ## 2019     Lochkovian    Lochkovian     419.2    410.8         6189
    ## 2085       Tremadoc      Tremadoc     485.4    477.7          521
    ## 2098       Tremadoc      Tremadoc     485.4    477.7          521
    ## 3336        Wenlock       Wenlock     433.4    427.4         7624
    ## 3395        Wenlock       Wenlock     433.4    427.4         7624
    ## 3408         Emsian      Eifelian     407.6    387.7         9677
    ## 5847       Tremadoc      Tremadoc     485.4    477.7        49841
    ## 5852       Tremadoc      Tremadoc     485.4    477.7        50356
    ##        primary_name primary_reso subgenus_name subgenus_reso  species_name
    ## 3    Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 613  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 614  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 658  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 851  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 955  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 975  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 984  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 988  Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 1049 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 1245 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 1358 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 1518 Acanthograptus         <NA>          <NA>          <NA> lejskoviensis
    ## 1792 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 2019 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 2085 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 2098 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 3336 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 3395 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 3408 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 5847 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ## 5852 Acanthograptus         <NA>          <NA>          <NA>           sp.
    ##      species_reso subgenus subgenus_no          genus genus_no family
    ## 3            <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 613          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 614          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 658          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 851          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 955          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 975          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 984          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 988          <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 1049         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 1245         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 1358         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 1518         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 1792         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 2019         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 2085         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 2098         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 3336         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 3395         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 3408         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 5847         <NA>       NA          NA Acanthograptus    33536   <NA>
    ## 5852         <NA>       NA          NA Acanthograptus    33536   <NA>
    ##      family_no      order order_no         class class_no       phylum
    ## 3           NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 613         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 614         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 658         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 851         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 955         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 975         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 984         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 988         NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 1049        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 1245        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 1358        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 1518        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 1792        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 2019        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 2085        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 2098        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3336        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3395        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 3408        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 5847        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ## 5852        NA Dendroidea    33535 Graptolithina    33534 Hemichordata
    ##      phylum_no    authorizer              enterer             modifier
    ## 3        33518  Sepkoski, J.          Sommers, M.              unknown
    ## 613      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 614      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 658      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 851      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 955      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 975      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 984      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 988      33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 1049     33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 1245     33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 1358     33518    Miller, A. Novack-Gottshall, P.              unknown
    ## 1518     33518    Miller, A.            Sessa, J.              unknown
    ## 1792     33518     Foote, M.            Foote, M.              unknown
    ## 2019     33518     Foote, M.            Foote, M.              unknown
    ## 2085     33518    Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2098     33518    Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 3336     33518     Foote, M.            Foote, M.              unknown
    ## 3395     33518     Foote, M.            Foote, M.              unknown
    ## 3408     33518     Foote, M.            Foote, M.              unknown
    ## 5847     33518 Kiessling, W.           Krause, M.              unknown
    ## 5852     33518 Kiessling, W.           Krause, M.              unknown
    ## 
    ## $Acrograptus
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 378          50981  occurrence      NA       NA          3706
    ## 380          50999  occurrence      NA       NA          3707
    ## 1332        118192  occurrence      NA       NA          8777
    ## 1380        118600  occurrence      NA       NA          8869
    ## 2651        264743  occurrence      NA       NA         20898
    ## 2699        265875  occurrence      NA       NA         21092
    ##      identified_name identified_rank identified_no taxonomic_reason
    ## 378  Acrograptus sp.           genus         33609             <NA>
    ## 380  Acrograptus sp.           genus         33609             <NA>
    ## 1332 Acrograptus sp.           genus         33609             <NA>
    ## 1380 Acrograptus sp.           genus         33609             <NA>
    ## 2651 Acrograptus sp.           genus         33609             <NA>
    ## 2699 Acrograptus sp.           genus         33609             <NA>
    ##      accepted_name accepted_rank accepted_no early_interval  late_interval
    ## 378    Acrograptus         genus       33609         Arenig         Arenig
    ## 380    Acrograptus         genus       33609 Early Llanvirn Early Llanvirn
    ## 1332   Acrograptus         genus       33609         Arenig         Arenig
    ## 1380   Acrograptus         genus       33609         Arenig         Arenig
    ## 2651   Acrograptus         genus       33609      Oretanian      Oretanian
    ## 2699   Acrograptus         genus       33609      Oretanian    Dobrotivian
    ##      early_age late_age reference_no primary_name primary_reso
    ## 378      478.6    466.0          173  Acrograptus         <NA>
    ## 380      466.0    463.5          173  Acrograptus         <NA>
    ## 1332     478.6    466.0          668  Acrograptus         <NA>
    ## 1380     478.6    466.0          600  Acrograptus         <NA>
    ## 2651     466.0    460.9         6366  Acrograptus         <NA>
    ## 2699     466.0    457.5         6395  Acrograptus         <NA>
    ##      subgenus_name subgenus_reso species_name species_reso subgenus
    ## 378           <NA>          <NA>          sp.         <NA>       NA
    ## 380           <NA>          <NA>          sp.         <NA>       NA
    ## 1332          <NA>          <NA>          sp.         <NA>       NA
    ## 1380          <NA>          <NA>          sp.         <NA>       NA
    ## 2651          <NA>          <NA>          sp.         <NA>       NA
    ## 2699          <NA>          <NA>          sp.         <NA>       NA
    ##      subgenus_no       genus genus_no family family_no        order
    ## 378           NA Acrograptus    33609   <NA>        NA Graptoloidea
    ## 380           NA Acrograptus    33609   <NA>        NA Graptoloidea
    ## 1332          NA Acrograptus    33609   <NA>        NA Graptoloidea
    ## 1380          NA Acrograptus    33609   <NA>        NA Graptoloidea
    ## 2651          NA Acrograptus    33609   <NA>        NA Graptoloidea
    ## 2699          NA Acrograptus    33609   <NA>        NA Graptoloidea
    ##      order_no         class class_no       phylum phylum_no authorizer
    ## 378     33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 380     33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 1332    33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 1380    33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 2651    33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 2699    33606 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ##                   enterer             modifier
    ## 378  Novack-Gottshall, P.              unknown
    ## 380  Novack-Gottshall, P.              unknown
    ## 1332 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 1380 Novack-Gottshall, P.              unknown
    ## 2651 Novack-Gottshall, P.           Wagner, P.
    ## 2699 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 
    ## $Adelograptus
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 187           9036  occurrence      NA       NA           415
    ## 337          49467  occurrence      NA       NA          3184
    ## 362          49933  occurrence      NA       NA          3306
    ## 367          50536  occurrence      NA       NA          3663
    ## 457         105361  occurrence      NA       NA          3109
    ## 461         105387  occurrence      NA       NA          4664
    ## 516         105464  occurrence      NA       NA          4675
    ## 615         106250  occurrence      NA       NA          4728
    ## 1124        108287  occurrence      NA       NA          7774
    ## 1242        108542  occurrence      NA       NA          7815
    ## 1379        118583  occurrence      NA       NA          8867
    ## 2099        240368  occurrence      NA       NA          7985
    ## 2106        240479  occurrence      NA       NA          7997
    ## 2116        240497  occurrence      NA       NA          8000
    ## 2135        240585  occurrence      NA       NA          8530
    ## 2305        242229  occurrence      NA       NA         21144
    ## 3610        596431  occurrence      NA       NA         63189
    ## 3628        596452  occurrence      NA       NA         63192
    ## 3631        596455  occurrence      NA       NA         63194
    ## 3633        596459  occurrence      NA       NA         63195
    ## 3668        596499  occurrence      NA       NA         63204
    ## 4223        826761  occurrence      NA       NA         91172
    ## 5337       1144019  occurrence      NA       NA        145616
    ## 5850       1196786  occurrence      NA       NA        154776
    ##                  identified_name identified_rank identified_no
    ## 187             Adelograptus sp.           genus         33537
    ## 337             Adelograptus sp.           genus         33537
    ## 362             Adelograptus sp.           genus         33537
    ## 367             Adelograptus sp.           genus         33537
    ## 457             Adelograptus sp.           genus         33537
    ## 461             Adelograptus sp.           genus         33537
    ## 516             Adelograptus sp.           genus         33537
    ## 615             Adelograptus sp.           genus         33537
    ## 1124            Adelograptus sp.           genus         33537
    ## 1242            Adelograptus sp.           genus         33537
    ## 1379            Adelograptus sp.           genus         33537
    ## 2099            Adelograptus sp.           genus         33537
    ## 2106            Adelograptus sp.           genus         33537
    ## 2116            Adelograptus sp.           genus         33537
    ## 2135            Adelograptus sp.           genus         33537
    ## 2305            Adelograptus sp.           genus         33537
    ## 3610         Adelograptus clarki         species         84009
    ## 3628            Adelograptus sp.           genus         33537
    ## 3631            Adelograptus sp.           genus         33537
    ## 3633         Adelograptus clarki         species         84009
    ## 3668            Adelograptus sp.           genus         33537
    ## 4223       Adelograptus antiquus         species         84007
    ## 5337 Adelograptus hunnebergensis         species         33537
    ## 5850            Adelograptus sp.           genus         33537
    ##             taxonomic_reason         accepted_name accepted_rank
    ## 187                     <NA>          Adelograptus         genus
    ## 337                     <NA>          Adelograptus         genus
    ## 362                     <NA>          Adelograptus         genus
    ## 367                     <NA>          Adelograptus         genus
    ## 457                     <NA>          Adelograptus         genus
    ## 461                     <NA>          Adelograptus         genus
    ## 516                     <NA>          Adelograptus         genus
    ## 615                     <NA>          Adelograptus         genus
    ## 1124                    <NA>          Adelograptus         genus
    ## 1242                    <NA>          Adelograptus         genus
    ## 1379                    <NA>          Adelograptus         genus
    ## 2099                    <NA>          Adelograptus         genus
    ## 2106                    <NA>          Adelograptus         genus
    ## 2116                    <NA>          Adelograptus         genus
    ## 2135                    <NA>          Adelograptus         genus
    ## 2305                    <NA>          Adelograptus         genus
    ## 3610                    <NA>   Adelograptus clarki       species
    ## 3628                    <NA>          Adelograptus         genus
    ## 3631                    <NA>          Adelograptus         genus
    ## 3633                    <NA>   Adelograptus clarki       species
    ## 3668                    <NA>          Adelograptus         genus
    ## 4223                    <NA> Adelograptus antiquus       species
    ## 5337 taxon not fully entered          Adelograptus         genus
    ## 5850                    <NA>          Adelograptus         genus
    ##      accepted_no early_interval late_interval early_age late_age
    ## 187        33537       Tremadoc      Tremadoc     485.4    477.7
    ## 337        33537         Arenig        Arenig     478.6    466.0
    ## 362        33537    Migneintian   Migneintian     485.4    478.6
    ## 367        33537     Cressagian    Cressagian     485.4    478.6
    ## 457        33537       Tremadoc      Tremadoc     485.4    477.7
    ## 461        33537       Tremadoc      Tremadoc     485.4    477.7
    ## 516        33537       Tremadoc      Tremadoc     485.4    477.7
    ## 615        33537       Tremadoc      Tremadoc     485.4    477.7
    ## 1124       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 1242       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 1379       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 2099       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 2106       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 2116       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 2135       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 2305       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 3610       84009    Tremadocian   Tremadocian     485.4    477.7
    ## 3628       33537  Lancefieldian   Bendigonian     485.4    473.9
    ## 3631       33537    Tremadocian   Tremadocian     485.4    477.7
    ## 3633       84009    Tremadocian   Tremadocian     485.4    477.7
    ## 3668       33537    Tremadocian   Tremadocian     485.4    477.7
    ## 4223       84007        Ibexian       Ibexian     488.3    471.8
    ## 5337       33537       Tremadoc      Tremadoc     485.4    477.7
    ## 5850       33537       Tremadoc      Tremadoc     485.4    477.7
    ##      reference_no primary_name primary_reso subgenus_name subgenus_reso
    ## 187            13 Adelograptus         <NA>          <NA>          <NA>
    ## 337           114 Adelograptus         <NA>          <NA>          <NA>
    ## 362           157 Adelograptus         <NA>          <NA>          <NA>
    ## 367           167 Adelograptus         <NA>          <NA>          <NA>
    ## 457           112 Adelograptus         <NA>          <NA>          <NA>
    ## 461           285 Adelograptus         <NA>          <NA>          <NA>
    ## 516           286 Adelograptus         <NA>          <NA>          <NA>
    ## 615           287 Adelograptus         <NA>          <NA>          <NA>
    ## 1124          480 Adelograptus         <NA>          <NA>          <NA>
    ## 1242          480 Adelograptus         <NA>          <NA>          <NA>
    ## 1379          600 Adelograptus         <NA>          <NA>          <NA>
    ## 2099          521 Adelograptus         <NA>          <NA>          <NA>
    ## 2106          521 Adelograptus         <NA>          <NA>          <NA>
    ## 2116          521 Adelograptus         <NA>          <NA>          <NA>
    ## 2135          522 Adelograptus         <NA>          <NA>          <NA>
    ## 2305         6478 Adelograptus         <NA>          <NA>          <NA>
    ## 3610        18179 Adelograptus         <NA>          <NA>          <NA>
    ## 3628        18179 Adelograptus         <NA>          <NA>          <NA>
    ## 3631        18179 Adelograptus         <NA>          <NA>          <NA>
    ## 3633        18179 Adelograptus         <NA>          <NA>          <NA>
    ## 3668        18179 Adelograptus         <NA>          <NA>          <NA>
    ## 4223        24434 Adelograptus         <NA>          <NA>          <NA>
    ## 5337        47089 Adelograptus         <NA>          <NA>          <NA>
    ## 5850        50356 Adelograptus         <NA>          <NA>          <NA>
    ##        species_name species_reso subgenus subgenus_no        genus
    ## 187             sp.         <NA>       NA          NA Adelograptus
    ## 337             sp.         <NA>       NA          NA Adelograptus
    ## 362             sp.         <NA>       NA          NA Adelograptus
    ## 367             sp.         <NA>       NA          NA Adelograptus
    ## 457             sp.         <NA>       NA          NA Adelograptus
    ## 461             sp.         <NA>       NA          NA Adelograptus
    ## 516             sp.         <NA>       NA          NA Adelograptus
    ## 615             sp.         <NA>       NA          NA Adelograptus
    ## 1124            sp.         <NA>       NA          NA Adelograptus
    ## 1242            sp.         <NA>       NA          NA Adelograptus
    ## 1379            sp.         <NA>       NA          NA Adelograptus
    ## 2099            sp.         <NA>       NA          NA Adelograptus
    ## 2106            sp.         <NA>       NA          NA Adelograptus
    ## 2116            sp.         <NA>       NA          NA Adelograptus
    ## 2135            sp.         <NA>       NA          NA Adelograptus
    ## 2305            sp.         <NA>       NA          NA Adelograptus
    ## 3610         clarki         <NA>       NA          NA Adelograptus
    ## 3628            sp.         <NA>       NA          NA Adelograptus
    ## 3631            sp.         <NA>       NA          NA Adelograptus
    ## 3633         clarki         <NA>       NA          NA Adelograptus
    ## 3668            sp.         <NA>       NA          NA Adelograptus
    ## 4223       antiquus         <NA>       NA          NA Adelograptus
    ## 5337 hunnebergensis         <NA>       NA          NA Adelograptus
    ## 5850            sp.         <NA>       NA          NA Adelograptus
    ##      genus_no family family_no      order order_no         class class_no
    ## 187     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 337     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 362     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 367     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 457     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 461     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 516     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 615     33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 1124    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 1242    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 1379    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 2099    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 2106    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 2116    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 2135    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 2305    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 3610    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 3628    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 3631    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 3633    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 3668    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 4223    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 5337    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ## 5850    33537   <NA>        NA Dendroidea    33535 Graptolithina    33534
    ##            phylum phylum_no    authorizer              enterer
    ## 187  Hemichordata     33518  Sepkoski, J.          Sommers, M.
    ## 337  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 362  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 367  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 457  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 461  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 516  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 615  Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 1124 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 1242 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 1379 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 2099 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 2106 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 2116 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 2135 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 2305 Hemichordata     33518    Miller, A. Novack-Gottshall, P.
    ## 3610 Hemichordata     33518     Hendy, A.            Hendy, A.
    ## 3628 Hemichordata     33518     Hendy, A.            Hendy, A.
    ## 3631 Hemichordata     33518     Hendy, A.            Hendy, A.
    ## 3633 Hemichordata     33518     Hendy, A.            Hendy, A.
    ## 3668 Hemichordata     33518     Hendy, A.            Hendy, A.
    ## 4223 Hemichordata     33518   Villier, L.          Villier, L.
    ## 5337 Hemichordata     33518 Kiessling, W.           Krause, M.
    ## 5850 Hemichordata     33518 Kiessling, W.           Krause, M.
    ##                  modifier
    ## 187               unknown
    ## 337               unknown
    ## 362               unknown
    ## 367               unknown
    ## 457               unknown
    ## 461               unknown
    ## 516               unknown
    ## 615               unknown
    ## 1124              unknown
    ## 1242              unknown
    ## 1379              unknown
    ## 2099 Novack-Gottshall, P.
    ## 2106 Novack-Gottshall, P.
    ## 2116 Novack-Gottshall, P.
    ## 2135 Novack-Gottshall, P.
    ## 2305 Novack-Gottshall, P.
    ## 3610            Hendy, A.
    ## 3628              unknown
    ## 3631            Hendy, A.
    ## 3633              unknown
    ## 3668              unknown
    ## 4223              unknown
    ## 5337              unknown
    ## 5850              unknown
    ## 
    ## $Airograptus
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 2281        242029  occurrence      NA       NA         20753
    ## 2298        242214  occurrence      NA       NA         21143
    ## 2300        242216  occurrence      NA       NA         21145
    ##      identified_name identified_rank identified_no taxonomic_reason
    ## 2281 Airograptus sp.           genus         88901             <NA>
    ## 2298 Airograptus sp.           genus         88901             <NA>
    ## 2300 Airograptus sp.           genus         88901             <NA>
    ##      accepted_name accepted_rank accepted_no early_interval late_interval
    ## 2281   Airograptus         genus       88901       Tremadoc      Tremadoc
    ## 2298   Airograptus         genus       88901       Tremadoc      Tremadoc
    ## 2300   Airograptus         genus       88901       Tremadoc      Tremadoc
    ##      early_age late_age reference_no primary_name primary_reso
    ## 2281     485.4    477.7         3861  Airograptus         <NA>
    ## 2298     485.4    477.7         6478  Airograptus         <NA>
    ## 2300     485.4    477.7         6478  Airograptus         <NA>
    ##      subgenus_name subgenus_reso species_name species_reso subgenus
    ## 2281          <NA>          <NA>          sp.         <NA>       NA
    ## 2298          <NA>          <NA>          sp.         <NA>       NA
    ## 2300          <NA>          <NA>          sp.         <NA>       NA
    ##      subgenus_no       genus genus_no family family_no      order order_no
    ## 2281          NA Airograptus    88901   <NA>        NA Dendroidea    33535
    ## 2298          NA Airograptus    88901   <NA>        NA Dendroidea    33535
    ## 2300          NA Airograptus    88901   <NA>        NA Dendroidea    33535
    ##              class class_no       phylum phylum_no authorizer
    ## 2281 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 2298 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ## 2300 Graptolithina    33534 Hemichordata     33518 Miller, A.
    ##                   enterer             modifier
    ## 2281 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2298 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2300 Novack-Gottshall, P. Novack-Gottshall, P.

    occFamily <- taxonSortPBDBocc(graptOccPBDB, rank = "family") # ...and for families
    head(occFamily)

    ## $Abrograptidae
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 1099        108256  occurrence      NA       NA          7770
    ## 2531        260375  occurrence      NA       NA         25169
    ## 2532        260376  occurrence      NA       NA         25169
    ## 2533        260377  occurrence      NA       NA         25169
    ##                        identified_name identified_rank identified_no
    ## 1099                Parabrograptus sp.           genus        114886
    ## 2531      Parabrograptus tribrachiatus         species        114888
    ## 2532 Parabrograptus tribrachiatus aff.         species        114888
    ## 2533  Parabrograptus tribrachiatus cf.         species        114888
    ##      taxonomic_reason                accepted_name accepted_rank
    ## 1099             <NA>               Parabrograptus         genus
    ## 2531             <NA> Parabrograptus tribrachiatus       species
    ## 2532             <NA> Parabrograptus tribrachiatus       species
    ## 2533             <NA> Parabrograptus tribrachiatus       species
    ##      accepted_no early_interval late_interval early_age late_age
    ## 1099      114886      Llandeilo     Llandeilo     466.0    449.5
    ## 2531      114888     Caradocian    Caradocian     460.9    449.5
    ## 2532      114888     Caradocian    Caradocian     460.9    449.5
    ## 2533      114888     Caradocian    Caradocian     460.9    449.5
    ##      reference_no   primary_name primary_reso subgenus_name subgenus_reso
    ## 1099          480 Parabrograptus         <NA>          <NA>          <NA>
    ## 2531         7064 Parabrograptus         <NA>          <NA>          <NA>
    ## 2532         7064 Parabrograptus         <NA>          <NA>          <NA>
    ## 2533         7064 Parabrograptus         <NA>          <NA>          <NA>
    ##       species_name species_reso subgenus subgenus_no          genus
    ## 1099           sp.         <NA>       NA          NA Parabrograptus
    ## 2531 tribrachiatus         <NA>       NA          NA Parabrograptus
    ## 2532 tribrachiatus         aff.       NA          NA Parabrograptus
    ## 2533 tribrachiatus          cf.       NA          NA Parabrograptus
    ##      genus_no        family family_no        order order_no         class
    ## 1099   114886 Abrograptidae    114887 Graptoloidea    33606 Graptolithina
    ## 2531   114886 Abrograptidae    114887 Graptoloidea    33606 Graptolithina
    ## 2532   114886 Abrograptidae    114887 Graptoloidea    33606 Graptolithina
    ## 2533   114886 Abrograptidae    114887 Graptoloidea    33606 Graptolithina
    ##      class_no       phylum phylum_no  authorizer              enterer
    ## 1099    33534 Hemichordata     33518  Miller, A. Novack-Gottshall, P.
    ## 2531    33534 Hemichordata     33518 Holland, S.           Hanson, T.
    ## 2532    33534 Hemichordata     33518 Holland, S.           Hanson, T.
    ## 2533    33534 Hemichordata     33518 Holland, S.           Hanson, T.
    ##      modifier
    ## 1099  unknown
    ## 2531  unknown
    ## 2532  unknown
    ## 2533  unknown
    ## 
    ## $Dendrograptidae
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 8             2343  occurrence      NA       NA           272
    ## 9             2391  occurrence      NA       NA           275
    ## 11            2420  occurrence      NA       NA           277
    ## 15            2451  occurrence      NA       NA           280
    ## 21            2561  occurrence      NA       NA           286
    ## 29            2760  occurrence      NA       NA           297
    ## 36            2799  occurrence      NA       NA           301
    ## 118           4922  occurrence      NA       NA           385
    ## 136           6203  occurrence      NA       NA           463
    ## 139           6305  occurrence      NA       NA           468
    ## 141           6486  occurrence      NA       NA           473
    ## 176           7978  occurrence      NA       NA           541
    ## 199           9798  occurrence      NA       NA           451
    ## 202          10248  occurrence      NA       NA           593
    ## 384          51064  occurrence      NA       NA          3711
    ## 387          51484  occurrence      NA       NA          3783
    ## 390          51541  occurrence      NA       NA          3841
    ## 434          77887  occurrence      NA       NA          5668
    ## 453         105298  occurrence      NA       NA          3105
    ## 460         105366  occurrence      NA       NA          3109
    ## 466         105393  occurrence      NA       NA          4664
    ## 606         106056  occurrence      NA       NA          4720
    ## 617         106254  occurrence      NA       NA          4728
    ## 620         106286  occurrence      NA       NA          4730
    ## 621         106322  occurrence      NA       NA          4735
    ## 622         106347  occurrence      NA       NA          4738
    ## 718         106888  occurrence      NA       NA          5423
    ## 757         107073  occurrence      NA       NA          7282
    ## 761         107086  occurrence      NA       NA          7290
    ## 784         107199  occurrence      NA       NA          7363
    ## 785         107202  occurrence      NA       NA          7364
    ## 786         107205  occurrence      NA       NA          7365
    ## 788         107211  occurrence      NA       NA          7367
    ## 789         107213  occurrence      NA       NA          7368
    ## 790         107217  occurrence      NA       NA          7369
    ## 807         107285  occurrence      NA       NA          7387
    ## 836         107396  occurrence      NA       NA          7653
    ## 884         107628  occurrence      NA       NA          7694
    ## 913         107688  occurrence      NA       NA          7702
    ## 916         107700  occurrence      NA       NA          7703
    ## 947         107743  occurrence      NA       NA          7712
    ## 957         107812  occurrence      NA       NA          7719
    ## 977         107883  occurrence      NA       NA          7727
    ## 985         107915  occurrence      NA       NA          7728
    ## 987         107939  occurrence      NA       NA          7729
    ## 990         107962  occurrence      NA       NA          7734
    ## 1052        108115  occurrence      NA       NA          7758
    ## 1128        108291  occurrence      NA       NA          7774
    ## 1137        108365  occurrence      NA       NA          7780
    ## 1168        108417  occurrence      NA       NA          7793
    ## 1246        108567  occurrence      NA       NA          7831
    ## 1289        108873  occurrence      NA       NA          7880
    ## 1300        108957  occurrence      NA       NA          7887
    ## 1303        109015  occurrence      NA       NA          7921
    ## 1343        118318  occurrence      NA       NA          8801
    ## 1344        118329  occurrence      NA       NA          8802
    ## 1345        118347  occurrence      NA       NA          8804
    ## 1346        118362  occurrence      NA       NA          8837
    ## 1347        118384  occurrence      NA       NA          8838
    ## 1348        118396  occurrence      NA       NA          8839
    ## 1351        118416  occurrence      NA       NA          8843
    ## 1377        118571  occurrence      NA       NA          8866
    ## 1382        118603  occurrence      NA       NA          8869
    ## 1395        118646  occurrence      NA       NA          8874
    ## 1451        118908  occurrence      NA       NA          9021
    ## 1455        118919  occurrence      NA       NA          9023
    ## 1492        131847  occurrence      NA       NA         10931
    ## 1536        140499  occurrence      NA       NA         12068
    ## 1537        140500  occurrence      NA       NA         12068
    ## 1538        140501  occurrence      NA       NA         12068
    ## 1539        140502  occurrence      NA       NA         12068
    ## 1546        141524  occurrence      NA       NA         12144
    ## 1547        141525  occurrence      NA       NA         12144
    ## 1548        141526  occurrence      NA       NA         12144
    ## 1551        141569  occurrence      NA       NA         12147
    ## 1552        141570  occurrence      NA       NA         12147
    ## 1562        147891  occurrence      NA       NA         13054
    ## 1784        156398  occurrence      NA       NA         13894
    ## 1791        156495  occurrence      NA       NA         13895
    ## 1974        159402  occurrence      NA       NA         14085
    ## 1981        159416  occurrence      NA       NA         14087
    ## 2030        160911  occurrence      NA       NA         14157
    ## 2045        161283  occurrence      NA       NA         14195
    ## 2091        240071  occurrence      NA       NA          7958
    ## 2095        240335  occurrence      NA       NA          7982
    ## 2097        240347  occurrence      NA       NA          7983
    ## 2105        240375  occurrence      NA       NA          7985
    ## 2109        240482  occurrence      NA       NA          7997
    ## 2269        241358  occurrence      NA       NA          9273
    ## 2271        241373  occurrence      NA       NA          9274
    ## 2273        241420  occurrence      NA       NA          9277
    ## 2275        241464  occurrence      NA       NA          9283
    ## 2277        241528  occurrence      NA       NA          9290
    ## 2280        242028  occurrence      NA       NA         20753
    ## 2283        242032  occurrence      NA       NA         20755
    ## 2297        242211  occurrence      NA       NA         21143
    ## 2302        242218  occurrence      NA       NA         21145
    ## 2308        242232  occurrence      NA       NA         21144
    ## 2396        243363  occurrence      NA       NA         23900
    ## 2397        243364  occurrence      NA       NA         23900
    ## 2438        254261  occurrence      NA       NA         12252
    ## 2439        254386  occurrence      NA       NA         12258
    ## 2487        255870  occurrence      NA       NA         24828
    ## 2635        264190  occurrence      NA       NA         20827
    ## 2639        264243  occurrence      NA       NA         20828
    ## 2673        265259  occurrence      NA       NA         20979
    ## 2684        265365  occurrence      NA       NA         20998
    ## 2829        279238  occurrence      NA       NA         26688
    ## 2833        282290  occurrence      NA       NA         26854
    ## 2834        282319  occurrence      NA       NA         26855
    ## 2835        282347  occurrence      NA       NA         26856
    ## 2840        282409  occurrence      NA       NA         26862
    ## 2847        282677  occurrence      NA       NA         26885
    ## 3098        290601  occurrence      NA       NA         27736
    ## 3118        290660  occurrence      NA       NA         27743
    ## 3334        292744  occurrence      NA       NA         27873
    ## 3393        293133  occurrence      NA       NA         27915
    ## 3400        293215  occurrence      NA       NA         27773
    ## 3536        490409  occurrence      NA       NA         25606
    ## 3629        596453  occurrence      NA       NA         63194
    ## 3666        596497  occurrence      NA       NA         63204
    ## 4028        621164  occurrence      NA       NA         66898
    ## 4029        621165  occurrence      NA       NA         66898
    ## 4030        621166  occurrence      NA       NA         66898
    ## 4031        621167  occurrence      NA       NA         66898
    ## 4033        640301  occurrence      NA       NA         69027
    ## 4036        642022  occurrence      NA       NA          9021
    ## 4037        670280  occurrence      NA       NA         72274
    ## 4052        703628  occurrence      NA       NA         75546
    ## 4083        712442  occurrence      NA       NA         76450
    ## 4084        712443  occurrence      NA       NA         76450
    ## 4085        712444  occurrence      NA       NA         76450
    ## 4119        717600  occurrence      NA       NA         77051
    ## 4122        717627  occurrence      NA       NA         77052
    ## 4126        717669  occurrence      NA       NA         77054
    ## 4129        717764  occurrence      NA       NA         77053
    ## 4133        718062  occurrence      NA       NA         77081
    ## 4154        727189  occurrence      NA       NA         78090
    ## 4172        765992  occurrence      NA       NA         81783
    ## 4173        766396  occurrence      NA       NA         81804
    ## 4177        766707  occurrence      NA       NA         81840
    ## 4178        767100  occurrence      NA       NA         81878
    ## 4179        767101  occurrence      NA       NA         81878
    ## 4182        767230  occurrence      NA       NA         81898
    ## 4187        770762  occurrence      NA       NA         82536
    ## 4189        770855  occurrence      NA       NA         82545
    ## 4190        770901  occurrence      NA       NA         82547
    ## 4191        770956  occurrence      NA       NA         82554
    ## 4192        770957  occurrence      NA       NA         82554
    ## 4195        770991  occurrence      NA       NA         82558
    ## 4196        770992  occurrence      NA       NA         82558
    ## 4199        771320  occurrence      NA       NA         82584
    ## 4200        771436  occurrence      NA       NA         82607
    ## 4201        771437  occurrence      NA       NA         82607
    ## 4204        774410  occurrence      NA       NA         83097
    ## 4205        774411  occurrence      NA       NA         83097
    ## 4241        914567  occurrence      NA       NA        103807
    ## 4242        914846  occurrence      NA       NA        103888
    ## 4245        914852  occurrence      NA       NA        103891
    ## 4246        914891  occurrence      NA       NA        103907
    ## 4251        914932  occurrence      NA       NA        103918
    ## 4294        918002  occurrence      NA       NA        104070
    ## 4295        918085  occurrence      NA       NA        104099
    ## 4300        924981  occurrence      NA       NA        105855
    ## 4499        969914  occurrence      NA       NA        114979
    ## 4511        975922  occurrence      NA       NA        116360
    ## 4544       1061483  occurrence      NA       NA        131106
    ## 4547       1063038  occurrence      NA       NA        131361
    ## 5854       1197328  occurrence      NA       NA        154882
    ## 5855       1209571  occurrence      NA       NA        156949
    ## 5856       1209572  occurrence      NA       NA        156950
    ## 5857       1209575  occurrence      NA       NA        156952
    ## 5858       1209576  occurrence      NA       NA        156953
    ## 5859       1209577  occurrence      NA       NA        156953
    ## 5860       1209578  occurrence      NA       NA        156954
    ## 5861       1209579  occurrence      NA       NA        156954
    ## 5862       1209583  occurrence      NA       NA        156956
    ## 5863       1209584  occurrence      NA       NA        156956
    ## 5864       1209585  occurrence      NA       NA        156957
    ## 5865       1209586  occurrence      NA       NA        156957
    ## 5866       1209587  occurrence      NA       NA        156957
    ## 5867       1209594  occurrence      NA       NA        156959
    ##                        identified_name identified_rank identified_no
    ## 8                       Dictyonema sp.           genus         33553
    ## 9                       Dictyonema sp.           genus         33553
    ## 11                      Dictyonema sp.           genus         33553
    ## 15            Dictyonema flabelliforme         species         33553
    ## 21                      Dictyonema sp.           genus         33553
    ## 29                      Dictyonema sp.           genus         33553
    ## 36                      Dictyonema sp.           genus         33553
    ## 118                     Dictyonema sp.           genus         33553
    ## 136                     Dictyonema sp.           genus         33553
    ## 139                     Dictyonema sp.           genus         33553
    ## 141                     Dictyonema sp.           genus         33553
    ## 176                     Dictyonema sp.           genus         33553
    ## 199                     Dictyonema sp.           genus         33553
    ## 202                     Dictyonema sp.           genus         33553
    ## 384                     Dictyonema sp.           genus         33553
    ## 387           Dictyonema flabelliforme         species         33553
    ## 390                     Dictyonema sp.           genus         33553
    ## 434             Dictyonema hamiltoniae         species         33553
    ## 453                     Dictyonema sp.           genus         33553
    ## 460                     Dictyonema sp.           genus         33553
    ## 466                     Dictyonema sp.           genus         33553
    ## 606                     Dictyonema sp.           genus         33553
    ## 617                     Dictyonema sp.           genus         33553
    ## 620                     Dictyonema sp.           genus         33553
    ## 621                     Dictyonema sp.           genus         33553
    ## 622                     Dictyonema sp.           genus         33553
    ## 718                     Dictyonema sp.           genus         33553
    ## 757                     Dictyonema sp.           genus         33553
    ## 761                     Dictyonema sp.           genus         33553
    ## 784                     Dictyonema sp.           genus         33553
    ## 785                     Dictyonema sp.           genus         33553
    ## 786                     Dictyonema sp.           genus         33553
    ## 788                     Dictyonema sp.           genus         33553
    ## 789                     Dictyonema sp.           genus         33553
    ## 790                     Dictyonema sp.           genus         33553
    ## 807                     Dictyonema sp.           genus         33553
    ## 836                     Dictyonema sp.           genus         33553
    ## 884                     Dictyonema sp.           genus         33553
    ## 913                     Dictyonema sp.           genus         33553
    ## 916                     Dictyonema sp.           genus         33553
    ## 947                     Dictyonema sp.           genus         33553
    ## 957                     Dictyonema sp.           genus         33553
    ## 977                     Dictyonema sp.           genus         33553
    ## 985                     Dictyonema sp.           genus         33553
    ## 987                     Dictyonema sp.           genus         33553
    ## 990                     Dictyonema sp.           genus         33553
    ## 1052                    Dictyonema sp.           genus         33553
    ## 1128                    Dictyonema sp.           genus         33553
    ## 1137                    Dictyonema sp.           genus         33553
    ## 1168                    Dictyonema sp.           genus         33553
    ## 1246                    Dictyonema sp.           genus         33553
    ## 1289                    Dictyonema sp.           genus         33553
    ## 1300                    Dictyonema sp.           genus         33553
    ## 1303                    Dictyonema sp.           genus         33553
    ## 1343                    Dictyonema sp.           genus         33553
    ## 1344                    Dictyonema sp.           genus         33553
    ## 1345                    Dictyonema sp.           genus         33553
    ## 1346                    Dictyonema sp.           genus         33553
    ## 1347                    Dictyonema sp.           genus         33553
    ## 1348                    Dictyonema sp.           genus         33553
    ## 1351                    Dictyonema sp.           genus         33553
    ## 1377                    Dictyonema sp.           genus         33553
    ## 1382                    Dictyonema sp.           genus         33553
    ## 1395                    Dictyonema sp.           genus         33553
    ## 1451          Dictyonema flabelliforme         species         33553
    ## 1455                    Dictyonema sp.           genus         33553
    ## 1492                    Dictyonema sp.           genus         33553
    ## 1536              Dictyonema elongatum         species         33553
    ## 1537            Dictyonema subregulare         species         33553
    ## 1538                Dictyonema subtile         species         33553
    ## 1539       Dictyonema crassibasale cf.         species         33553
    ## 1546               Dictyonema pragense         species         33553
    ## 1547              Dictyonema goepperti         species         33553
    ## 1548                    Dictyonema sp.           genus         33553
    ## 1551               Dictyonema pragense         species         33553
    ## 1552              Dictyonema goepperti         species         33553
    ## 1562                    Dictyonema sp.           genus         33553
    ## 1784              Dictyonema elongatum         species         33553
    ## 1791                    Dictyonema sp.           genus         33553
    ## 1974           Dictyonema hyskovicense         species         33553
    ## 1981                    Dictyonema sp.           genus         33553
    ## 2030 Dictyonema (Dictyonema) elongatum         species         33553
    ## 2045                    Dictyonema sp.           genus         33553
    ## 2091                    Dictyonema sp.           genus         33553
    ## 2095                    Dictyonema sp.           genus         33553
    ## 2097                    Dictyonema sp.           genus         33553
    ## 2105                    Dictyonema sp.           genus         33553
    ## 2109                    Dictyonema sp.           genus         33553
    ## 2269                    Dictyonema sp.           genus         33553
    ## 2271                    Dictyonema sp.           genus         33553
    ## 2273                    Dictyonema sp.           genus         33553
    ## 2275                    Dictyonema sp.           genus         33553
    ## 2277                    Dictyonema sp.           genus         33553
    ## 2280                    Dictyonema sp.           genus         33553
    ## 2283                    Dictyonema sp.           genus         33553
    ## 2297                    Dictyonema sp.           genus         33553
    ## 2302                    Dictyonema sp.           genus         33553
    ## 2308                    Dictyonema sp.           genus         33553
    ## 2396             Dictyonema francesiae         species         33553
    ## 2397      Dictyonema rockcrossingensis         species         33553
    ## 2438                    Dictyonema sp.           genus         33553
    ## 2439                    Dictyonema sp.           genus         33553
    ## 2487                    Dictyonema sp.           genus         33553
    ## 2635                    Dictyonema sp.           genus         33553
    ## 2639                    Dictyonema sp.           genus         33553
    ## 2673                    Dictyonema sp.           genus         33553
    ## 2684                    Dictyonema sp.           genus         33553
    ## 2829                    Dictyonema sp.           genus         33553
    ## 2833              Dictyonema retiforme         species         33553
    ## 2834                    Dictyonema sp.           genus         33553
    ## 2835                    Dictyonema sp.           genus         33553
    ## 2840                    Dictyonema sp.           genus         33553
    ## 2847                    Dictyonema sp.           genus         33553
    ## 3098                    Dictyonema sp.           genus         33553
    ## 3118                    Dictyonema sp.           genus         33553
    ## 3334                    Dictyonema sp.           genus         33553
    ## 3393                    Dictyonema sp.           genus         33553
    ## 3400          Dictyonema desmoides cf.         species         33553
    ## 3536                    Dictyonema sp.           genus         33553
    ## 3629             Dictyonema pulchellum         species         84004
    ## 3666             Dictyonema pulchellum         species         84004
    ## 4028         Dictyonema sp. A informal           genus         33553
    ## 4029         Dictyonema sp. B informal           genus         33553
    ## 4030         Dictyonema sp. C informal           genus         33553
    ## 4031         Dictyonema sp. D informal           genus         33553
    ## 4033  Dictyonema sp. undet. 1 informal         species         33553
    ## 4036                    Dictyonema sp.           genus         33553
    ## 4037                    Dictyonema sp.           genus         33553
    ## 4052                    Dictyonema sp.           genus         33553
    ## 4083           Dictyonema crassibasale         species         33553
    ## 4084              Dictyonema retiforme         species         33553
    ## 4085               Dictyonema tenellum         species         33553
    ## 4119                    Dictyonema sp.           genus         33553
    ## 4122               Dictyonema gracilis         species         33553
    ## 4126               Dictyonema gracilis         species         33553
    ## 4129               Dictyonema gracilis         species         33553
    ## 4133                    Dictyonema sp.           genus         33553
    ## 4154                    Dictyonema sp.           genus         33553
    ## 4172              Dictyonema retiforme         species         33553
    ## 4173              Dictyonema retiforme         species         33553
    ## 4177           Dictyonema subretiforme         species         33553
    ## 4178                Dictyonema gracile         species         33553
    ## 4179              Dictyonema retiforme         species         33553
    ## 4182              Dictyonema retiforme         species         33553
    ## 4187           Dictyonema subretiforme         species         33553
    ## 4189               Dictyonema gracilis         species         33553
    ## 4190               Dictyonema gracilis         species         33553
    ## 4191               Dictyonema gracilis         species         33553
    ## 4192              Dictyonema retiforme         species         33553
    ## 4195               Dictyonema gracilis         species         33553
    ## 4196              Dictyonema retiforme         species         33553
    ## 4199              Dictyonema retiforme         species         33553
    ## 4200               Dictyonema gracilis         species         33553
    ## 4201              Dictyonema retiforme         species         33553
    ## 4204               Dictyonema gracilis         species         33553
    ## 4205              Dictyonema retiforme         species         33553
    ## 4241                    Dictyonema sp.           genus         33553
    ## 4242      Dictyonema flabelliforme cf.         species         33553
    ## 4245      Dictyonema flabelliforme cf.         species         33553
    ## 4246      Dictyonema flabelliforme cf.         species         33553
    ## 4251                    Dictyonema sp.           genus         33553
    ## 4294                    Dictyonema sp.           genus         33553
    ## 4295                    Dictyonema sp.           genus         33553
    ## 4300          Dictyonema flabelliforme         species         33553
    ## 4499                    Dictyonema sp.           genus         33553
    ## 4511                    Dictyonema sp.           genus         33553
    ## 4544          Dictyonema flabelliforme         species         33553
    ## 4547             Dictyonema quebecense         species         33553
    ## 5854                    Dictyonema sp.           genus         33553
    ## 5855           Dictyonema praeparabola         species         33553
    ## 5856           Dictyonema praeparabola         species         33553
    ## 5857                Dictyonema sociale         species         33553
    ## 5858                Dictyonema sociale         species         33553
    ## 5859               Dictyonema parabola         species         33553
    ## 5860                Dictyonema sociale         species         33553
    ## 5861               Dictyonema parabola         species         33553
    ## 5862                Dictyonema sociale         species         33553
    ## 5863               Dictyonema parabola         species         33553
    ## 5864                Dictyonema sociale         species         33553
    ## 5865               Dictyonema parabola         species         33553
    ## 5866          Dictyonema flabelliforme         species         33553
    ## 5867                    Dictyonema sp.           genus         33553
    ##             taxonomic_reason         accepted_name accepted_rank
    ## 8                       <NA>            Dictyonema         genus
    ## 9                       <NA>            Dictyonema         genus
    ## 11                      <NA>            Dictyonema         genus
    ## 15   taxon not fully entered            Dictyonema         genus
    ## 21                      <NA>            Dictyonema         genus
    ## 29                      <NA>            Dictyonema         genus
    ## 36                      <NA>            Dictyonema         genus
    ## 118                     <NA>            Dictyonema         genus
    ## 136                     <NA>            Dictyonema         genus
    ## 139                     <NA>            Dictyonema         genus
    ## 141                     <NA>            Dictyonema         genus
    ## 176                     <NA>            Dictyonema         genus
    ## 199                     <NA>            Dictyonema         genus
    ## 202                     <NA>            Dictyonema         genus
    ## 384                     <NA>            Dictyonema         genus
    ## 387  taxon not fully entered            Dictyonema         genus
    ## 390                     <NA>            Dictyonema         genus
    ## 434  taxon not fully entered            Dictyonema         genus
    ## 453                     <NA>            Dictyonema         genus
    ## 460                     <NA>            Dictyonema         genus
    ## 466                     <NA>            Dictyonema         genus
    ## 606                     <NA>            Dictyonema         genus
    ## 617                     <NA>            Dictyonema         genus
    ## 620                     <NA>            Dictyonema         genus
    ## 621                     <NA>            Dictyonema         genus
    ## 622                     <NA>            Dictyonema         genus
    ## 718                     <NA>            Dictyonema         genus
    ## 757                     <NA>            Dictyonema         genus
    ## 761                     <NA>            Dictyonema         genus
    ## 784                     <NA>            Dictyonema         genus
    ## 785                     <NA>            Dictyonema         genus
    ## 786                     <NA>            Dictyonema         genus
    ## 788                     <NA>            Dictyonema         genus
    ## 789                     <NA>            Dictyonema         genus
    ## 790                     <NA>            Dictyonema         genus
    ## 807                     <NA>            Dictyonema         genus
    ## 836                     <NA>            Dictyonema         genus
    ## 884                     <NA>            Dictyonema         genus
    ## 913                     <NA>            Dictyonema         genus
    ## 916                     <NA>            Dictyonema         genus
    ## 947                     <NA>            Dictyonema         genus
    ## 957                     <NA>            Dictyonema         genus
    ## 977                     <NA>            Dictyonema         genus
    ## 985                     <NA>            Dictyonema         genus
    ## 987                     <NA>            Dictyonema         genus
    ## 990                     <NA>            Dictyonema         genus
    ## 1052                    <NA>            Dictyonema         genus
    ## 1128                    <NA>            Dictyonema         genus
    ## 1137                    <NA>            Dictyonema         genus
    ## 1168                    <NA>            Dictyonema         genus
    ## 1246                    <NA>            Dictyonema         genus
    ## 1289                    <NA>            Dictyonema         genus
    ## 1300                    <NA>            Dictyonema         genus
    ## 1303                    <NA>            Dictyonema         genus
    ## 1343                    <NA>            Dictyonema         genus
    ## 1344                    <NA>            Dictyonema         genus
    ## 1345                    <NA>            Dictyonema         genus
    ## 1346                    <NA>            Dictyonema         genus
    ## 1347                    <NA>            Dictyonema         genus
    ## 1348                    <NA>            Dictyonema         genus
    ## 1351                    <NA>            Dictyonema         genus
    ## 1377                    <NA>            Dictyonema         genus
    ## 1382                    <NA>            Dictyonema         genus
    ## 1395                    <NA>            Dictyonema         genus
    ## 1451 taxon not fully entered            Dictyonema         genus
    ## 1455                    <NA>            Dictyonema         genus
    ## 1492                    <NA>            Dictyonema         genus
    ## 1536 taxon not fully entered            Dictyonema         genus
    ## 1537 taxon not fully entered            Dictyonema         genus
    ## 1538 taxon not fully entered            Dictyonema         genus
    ## 1539 taxon not fully entered            Dictyonema         genus
    ## 1546 taxon not fully entered            Dictyonema         genus
    ## 1547 taxon not fully entered            Dictyonema         genus
    ## 1548                    <NA>            Dictyonema         genus
    ## 1551 taxon not fully entered            Dictyonema         genus
    ## 1552 taxon not fully entered            Dictyonema         genus
    ## 1562                    <NA>            Dictyonema         genus
    ## 1784 taxon not fully entered            Dictyonema         genus
    ## 1791                    <NA>            Dictyonema         genus
    ## 1974 taxon not fully entered            Dictyonema         genus
    ## 1981                    <NA>            Dictyonema         genus
    ## 2030 taxon not fully entered            Dictyonema         genus
    ## 2045                    <NA>            Dictyonema         genus
    ## 2091                    <NA>            Dictyonema         genus
    ## 2095                    <NA>            Dictyonema         genus
    ## 2097                    <NA>            Dictyonema         genus
    ## 2105                    <NA>            Dictyonema         genus
    ## 2109                    <NA>            Dictyonema         genus
    ## 2269                    <NA>            Dictyonema         genus
    ## 2271                    <NA>            Dictyonema         genus
    ## 2273                    <NA>            Dictyonema         genus
    ## 2275                    <NA>            Dictyonema         genus
    ## 2277                    <NA>            Dictyonema         genus
    ## 2280                    <NA>            Dictyonema         genus
    ## 2283                    <NA>            Dictyonema         genus
    ## 2297                    <NA>            Dictyonema         genus
    ## 2302                    <NA>            Dictyonema         genus
    ## 2308                    <NA>            Dictyonema         genus
    ## 2396 taxon not fully entered            Dictyonema         genus
    ## 2397 taxon not fully entered            Dictyonema         genus
    ## 2438                    <NA>            Dictyonema         genus
    ## 2439                    <NA>            Dictyonema         genus
    ## 2487                    <NA>            Dictyonema         genus
    ## 2635                    <NA>            Dictyonema         genus
    ## 2639                    <NA>            Dictyonema         genus
    ## 2673                    <NA>            Dictyonema         genus
    ## 2684                    <NA>            Dictyonema         genus
    ## 2829                    <NA>            Dictyonema         genus
    ## 2833 taxon not fully entered            Dictyonema         genus
    ## 2834                    <NA>            Dictyonema         genus
    ## 2835                    <NA>            Dictyonema         genus
    ## 2840                    <NA>            Dictyonema         genus
    ## 2847                    <NA>            Dictyonema         genus
    ## 3098                    <NA>            Dictyonema         genus
    ## 3118                    <NA>            Dictyonema         genus
    ## 3334                    <NA>            Dictyonema         genus
    ## 3393                    <NA>            Dictyonema         genus
    ## 3400 taxon not fully entered            Dictyonema         genus
    ## 3536                    <NA>            Dictyonema         genus
    ## 3629                    <NA> Dictyonema pulchellum       species
    ## 3666                    <NA> Dictyonema pulchellum       species
    ## 4028 taxon not fully entered            Dictyonema         genus
    ## 4029 taxon not fully entered            Dictyonema         genus
    ## 4030 taxon not fully entered            Dictyonema         genus
    ## 4031 taxon not fully entered            Dictyonema         genus
    ## 4033 taxon not fully entered            Dictyonema         genus
    ## 4036                    <NA>            Dictyonema         genus
    ## 4037                    <NA>            Dictyonema         genus
    ## 4052                    <NA>            Dictyonema         genus
    ## 4083 taxon not fully entered            Dictyonema         genus
    ## 4084 taxon not fully entered            Dictyonema         genus
    ## 4085 taxon not fully entered            Dictyonema         genus
    ## 4119                    <NA>            Dictyonema         genus
    ## 4122 taxon not fully entered            Dictyonema         genus
    ## 4126 taxon not fully entered            Dictyonema         genus
    ## 4129 taxon not fully entered            Dictyonema         genus
    ## 4133                    <NA>            Dictyonema         genus
    ## 4154                    <NA>            Dictyonema         genus
    ## 4172 taxon not fully entered            Dictyonema         genus
    ## 4173 taxon not fully entered            Dictyonema         genus
    ## 4177 taxon not fully entered            Dictyonema         genus
    ## 4178 taxon not fully entered            Dictyonema         genus
    ## 4179 taxon not fully entered            Dictyonema         genus
    ## 4182 taxon not fully entered            Dictyonema         genus
    ## 4187 taxon not fully entered            Dictyonema         genus
    ## 4189 taxon not fully entered            Dictyonema         genus
    ## 4190 taxon not fully entered            Dictyonema         genus
    ## 4191 taxon not fully entered            Dictyonema         genus
    ## 4192 taxon not fully entered            Dictyonema         genus
    ## 4195 taxon not fully entered            Dictyonema         genus
    ## 4196 taxon not fully entered            Dictyonema         genus
    ## 4199 taxon not fully entered            Dictyonema         genus
    ## 4200 taxon not fully entered            Dictyonema         genus
    ## 4201 taxon not fully entered            Dictyonema         genus
    ## 4204 taxon not fully entered            Dictyonema         genus
    ## 4205 taxon not fully entered            Dictyonema         genus
    ## 4241                    <NA>            Dictyonema         genus
    ## 4242 taxon not fully entered            Dictyonema         genus
    ## 4245 taxon not fully entered            Dictyonema         genus
    ## 4246 taxon not fully entered            Dictyonema         genus
    ## 4251                    <NA>            Dictyonema         genus
    ## 4294                    <NA>            Dictyonema         genus
    ## 4295                    <NA>            Dictyonema         genus
    ## 4300 taxon not fully entered            Dictyonema         genus
    ## 4499                    <NA>            Dictyonema         genus
    ## 4511                    <NA>            Dictyonema         genus
    ## 4544 taxon not fully entered            Dictyonema         genus
    ## 4547 taxon not fully entered            Dictyonema         genus
    ## 5854                    <NA>            Dictyonema         genus
    ## 5855 taxon not fully entered            Dictyonema         genus
    ## 5856 taxon not fully entered            Dictyonema         genus
    ## 5857 taxon not fully entered            Dictyonema         genus
    ## 5858 taxon not fully entered            Dictyonema         genus
    ## 5859 taxon not fully entered            Dictyonema         genus
    ## 5860 taxon not fully entered            Dictyonema         genus
    ## 5861 taxon not fully entered            Dictyonema         genus
    ## 5862 taxon not fully entered            Dictyonema         genus
    ## 5863 taxon not fully entered            Dictyonema         genus
    ## 5864 taxon not fully entered            Dictyonema         genus
    ## 5865 taxon not fully entered            Dictyonema         genus
    ## 5866 taxon not fully entered            Dictyonema         genus
    ## 5867                    <NA>            Dictyonema         genus
    ##      accepted_no early_interval  late_interval early_age late_age
    ## 8          33553       Tremadoc       Tremadoc     485.4    477.7
    ## 9          33553       Tremadoc       Tremadoc     485.4    477.7
    ## 11         33553       Tremadoc       Tremadoc     485.4    477.7
    ## 15         33553       Tremadoc       Tremadoc     485.4    477.7
    ## 21         33553         Arenig         Arenig     478.6    466.0
    ## 29         33553   Whiterockian   Whiterockian     471.8    457.5
    ## 36         33553   Whiterockian   Whiterockian     471.8    457.5
    ## 118        33553        Edenian        Edenian     460.9    449.5
    ## 136        33553     Llandovery     Llandovery     443.4    433.4
    ## 139        33553       Silurian       Silurian     443.4    419.2
    ## 141        33553        Wenlock        Wenlock     433.4    427.4
    ## 176        33553        Wenlock        Wenlock     433.4    427.4
    ## 199        33553     Llandovery     Llandovery     443.4    433.4
    ## 202        33553     Lochkovian     Lochkovian     419.2    410.8
    ## 384        33553     Cressagian     Cressagian     485.4    478.6
    ## 387        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 390        33553        Klabava        Klabava     478.6    466.0
    ## 434        33553       Givetian       Givetian     387.7    382.7
    ## 453        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 460        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 466        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 606        33553         Arenig         Arenig     478.6    466.0
    ## 617        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 620        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 621        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 622        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 718        33553 Early Llanvirn Early Llanvirn     466.0    463.5
    ## 757        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 761        33553 Early Llanvirn Early Llanvirn     466.0    463.5
    ## 784        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 785        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 786        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 788        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 789        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 790        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 807        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 836        33553         Wufeng     Hirnantian     449.5    443.4
    ## 884        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 913        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 916        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 947        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 957        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 977        33553          Dawan          Dawan     478.6    468.1
    ## 985        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 987        33553       Tremadoc       Tremadoc     485.4    477.7
    ## 990        33553         Arenig         Arenig     478.6    466.0
    ## 1052       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1128       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1137       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1168       33553        Ashgill        Ashgill     449.5    443.7
    ## 1246       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1289       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1300       33553         Arenig         Arenig     478.6    466.0
    ## 1303       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1343       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1344       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1345       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1346       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1347       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1348       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1351       33553         Arenig         Arenig     478.6    466.0
    ## 1377       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1382       33553         Arenig         Arenig     478.6    466.0
    ## 1395       33553      Costonian      Costonian     460.9    457.5
    ## 1451       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1455       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 1492       33553        Pridoli        Pridoli     423.0    419.2
    ## 1536       33553     Lochkovian     Lochkovian     419.2    410.8
    ## 1537       33553     Lochkovian     Lochkovian     419.2    410.8
    ## 1538       33553     Lochkovian     Lochkovian     419.2    410.8
    ## 1539       33553     Lochkovian     Lochkovian     419.2    410.8
    ## 1546       33553     Zlichovian         Daleje     409.1    388.1
    ## 1547       33553     Zlichovian         Daleje     409.1    388.1
    ## 1548       33553     Zlichovian         Daleje     409.1    388.1
    ## 1551       33553     Zlichovian         Daleje     409.1    388.1
    ## 1552       33553     Zlichovian         Daleje     409.1    388.1
    ## 1562       33553        Wenlock        Wenlock     433.4    427.4
    ## 1784       33553        Pridoli        Pridoli     423.0    419.2
    ## 1791       33553     Lochkovian     Lochkovian     419.2    410.8
    ## 1974       33553       Aeronian       Aeronian     440.8    438.5
    ## 1981       33553       Aeronian       Aeronian     440.8    438.5
    ## 2030       33553        Pridoli        Pridoli     423.0    419.2
    ## 2045       33553        Wenlock        Wenlock     433.4    427.4
    ## 2091       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2095       33553         Arenig         Arenig     478.6    466.0
    ## 2097       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2105       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2109       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2269       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2271       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2273       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2275       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2277       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2280       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2283       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2297       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2302       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2308       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2396       33553   Blackriveran   Blackriveran     460.9    449.5
    ## 2397       33553   Blackriveran   Blackriveran     460.9    449.5
    ## 2438       33553       Eifelian       Eifelian     393.3    387.7
    ## 2439       33553       Eifelian       Givetian     393.3    382.7
    ## 2487       33553       Ontarian       Ontarian     439.0    428.2
    ## 2635       33553         Arenig         Arenig     478.6    466.0
    ## 2639       33553         Arenig         Arenig     478.6    466.0
    ## 2673       33553         Arenig         Arenig     478.6    466.0
    ## 2684       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 2829       33553         Ludlow         Ludlow     427.4    423.0
    ## 2833       33553        Wenlock        Wenlock     433.4    427.4
    ## 2834       33553        Wenlock        Wenlock     433.4    427.4
    ## 2835       33553        Wenlock        Wenlock     433.4    427.4
    ## 2840       33553   Sheinwoodian   Sheinwoodian     433.4    430.5
    ## 2847       33553     Llandovery     Llandovery     443.4    433.4
    ## 3098       33553     Llandovery     Llandovery     443.4    433.4
    ## 3118       33553      Telychian      Telychian     438.5    433.4
    ## 3334       33553        Wenlock        Wenlock     433.4    427.4
    ## 3393       33553        Wenlock        Wenlock     433.4    427.4
    ## 3400       33553      Telychian      Telychian     438.5    433.4
    ## 3536       33553      Merioneth      Merioneth     501.0    485.4
    ## 3629       84004    Tremadocian    Tremadocian     485.4    477.7
    ## 3666       84004    Tremadocian    Tremadocian     485.4    477.7
    ## 4028       33553       Givetian       Givetian     387.7    382.7
    ## 4029       33553       Givetian       Givetian     387.7    382.7
    ## 4030       33553       Givetian       Givetian     387.7    382.7
    ## 4031       33553       Givetian       Givetian     387.7    382.7
    ## 4033       33553      Demingian      Demingian     485.4    478.6
    ## 4036       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 4037       33553      Furongian       Tremadoc     497.0    477.7
    ## 4052       33553         Wufeng         Wufeng     449.5    443.7
    ## 4083       33553         Ludlow         Ludlow     427.4    423.0
    ## 4084       33553         Ludlow         Ludlow     427.4    423.0
    ## 4085       33553         Ludlow         Ludlow     427.4    423.0
    ## 4119       33553     Llandovery     Llandovery     443.4    433.4
    ## 4122       33553     Llandovery     Llandovery     443.4    433.4
    ## 4126       33553     Llandovery     Llandovery     443.4    433.4
    ## 4129       33553     Llandovery     Llandovery     443.4    433.4
    ## 4133       33553     Llandovery     Llandovery     443.4    433.4
    ## 4154       33553       Tremadoc       Tremadoc     485.4    477.7
    ## 4172       33553        Wenlock        Wenlock     433.4    427.4
    ## 4173       33553        Wenlock        Wenlock     433.4    427.4
    ## 4177       33553        Wenlock        Wenlock     433.4    427.4
    ## 4178       33553      Telychian      Telychian     438.5    433.4
    ## 4179       33553      Telychian      Telychian     438.5    433.4
    ## 4182       33553        Wenlock        Wenlock     433.4    427.4
    ## 4187       33553   Sheinwoodian   Sheinwoodian     433.4    430.5
    ## 4189       33553   Sheinwoodian   Sheinwoodian     433.4    430.5
    ## 4190       33553       Aeronian       Aeronian     440.8    438.5
    ## 4191       33553      Telychian      Telychian     438.5    433.4
    ## 4192       33553      Telychian      Telychian     438.5    433.4
    ## 4195       33553      Telychian      Telychian     438.5    433.4
    ## 4196       33553      Telychian      Telychian     438.5    433.4
    ## 4199       33553   Sheinwoodian   Sheinwoodian     433.4    430.5
    ## 4200       33553      Telychian      Telychian     438.5    433.4
    ## 4201       33553      Telychian      Telychian     438.5    433.4
    ## 4204       33553      Telychian      Telychian     438.5    433.4
    ## 4205       33553      Telychian      Telychian     438.5    433.4
    ## 4241       33553       Canadian       Canadian     485.4    468.1
    ## 4242       33553  Blackhillsian  Blackhillsian     478.6    471.8
    ## 4245       33553       Canadian       Canadian     485.4    468.1
    ## 4246       33553       Canadian       Canadian     485.4    468.1
    ## 4251       33553       Canadian       Canadian     485.4    468.1
    ## 4294       33553         Tulean         Tulean     485.4    471.8
    ## 4295       33553         Tulean         Tulean     485.4    471.8
    ## 4300       33553    Tremadocian    Tremadocian     485.4    477.7
    ## 4499       33553       Cambrian       Cambrian     541.0    485.4
    ## 4511       33553      Furongian      Furongian     497.0    485.4
    ## 4544       33553     Niuchehean     Niuchehean     498.5    485.4
    ## 4547       33553     Niuchehean     Niuchehean     498.5    485.4
    ## 5854       33553       Tremadoc         Floian     485.4    470.0
    ## 5855       33553     Ordovician     Ordovician     485.4    443.4
    ## 5856       33553     Ordovician     Ordovician     485.4    443.4
    ## 5857       33553     Ordovician     Ordovician     485.4    443.4
    ## 5858       33553     Ordovician     Ordovician     485.4    443.4
    ## 5859       33553     Ordovician     Ordovician     485.4    443.4
    ## 5860       33553     Ordovician     Ordovician     485.4    443.4
    ## 5861       33553     Ordovician     Ordovician     485.4    443.4
    ## 5862       33553     Ordovician     Ordovician     485.4    443.4
    ## 5863       33553     Ordovician     Ordovician     485.4    443.4
    ## 5864       33553     Ordovician     Ordovician     485.4    443.4
    ## 5865       33553     Ordovician     Ordovician     485.4    443.4
    ## 5866       33553     Ordovician     Ordovician     485.4    443.4
    ## 5867       33553     Ordovician     Ordovician     485.4    443.4
    ##      reference_no primary_name primary_reso subgenus_name subgenus_reso
    ## 8              13   Dictyonema         <NA>          <NA>          <NA>
    ## 9              13   Dictyonema         <NA>          <NA>          <NA>
    ## 11             13   Dictyonema         <NA>          <NA>          <NA>
    ## 15             13   Dictyonema         <NA>          <NA>          <NA>
    ## 21             13   Dictyonema         <NA>          <NA>          <NA>
    ## 29             13   Dictyonema         <NA>          <NA>          <NA>
    ## 36             13   Dictyonema         <NA>          <NA>          <NA>
    ## 118            13   Dictyonema         <NA>          <NA>          <NA>
    ## 136            13   Dictyonema         <NA>          <NA>          <NA>
    ## 139            13   Dictyonema         <NA>          <NA>          <NA>
    ## 141            13   Dictyonema         <NA>          <NA>          <NA>
    ## 176            13   Dictyonema         <NA>          <NA>          <NA>
    ## 199            13   Dictyonema         <NA>          <NA>          <NA>
    ## 202            13   Dictyonema         <NA>          <NA>          <NA>
    ## 384           177   Dictyonema         <NA>          <NA>          <NA>
    ## 387           227   Dictyonema         <NA>          <NA>          <NA>
    ## 390           227   Dictyonema         <NA>          <NA>          <NA>
    ## 434           347   Dictyonema         <NA>          <NA>          <NA>
    ## 453           110   Dictyonema         <NA>          <NA>          <NA>
    ## 460           112   Dictyonema         <NA>          <NA>          <NA>
    ## 466           285   Dictyonema         <NA>          <NA>          <NA>
    ## 606           287   Dictyonema         <NA>          <NA>          <NA>
    ## 617           287   Dictyonema         <NA>          <NA>          <NA>
    ## 620           287   Dictyonema         <NA>          <NA>          <NA>
    ## 621           287   Dictyonema         <NA>          <NA>          <NA>
    ## 622           287   Dictyonema         <NA>          <NA>          <NA>
    ## 718           288   Dictyonema         <NA>          <NA>          <NA>
    ## 757           288   Dictyonema         <NA>          <NA>          <NA>
    ## 761           288   Dictyonema         <NA>          <NA>          <NA>
    ## 784           288   Dictyonema         <NA>          <NA>          <NA>
    ## 785           288   Dictyonema         <NA>          <NA>          <NA>
    ## 786           288   Dictyonema         <NA>          <NA>          <NA>
    ## 788           288   Dictyonema         <NA>          <NA>          <NA>
    ## 789           288   Dictyonema         <NA>          <NA>          <NA>
    ## 790           288   Dictyonema         <NA>          <NA>          <NA>
    ## 807           475   Dictyonema         <NA>          <NA>          <NA>
    ## 836           485   Dictyonema         <NA>          <NA>          <NA>
    ## 884           476   Dictyonema         <NA>          <NA>          <NA>
    ## 913           476   Dictyonema         <NA>          <NA>          <NA>
    ## 916           476   Dictyonema         <NA>          <NA>          <NA>
    ## 947           476   Dictyonema         <NA>          <NA>          <NA>
    ## 957           477   Dictyonema         <NA>          <NA>          <NA>
    ## 977           477   Dictyonema         <NA>          <NA>          <NA>
    ## 985           477   Dictyonema         <NA>          <NA>          <NA>
    ## 987           477   Dictyonema         <NA>          <NA>          <NA>
    ## 990           478   Dictyonema         <NA>          <NA>          <NA>
    ## 1052          479   Dictyonema         <NA>          <NA>          <NA>
    ## 1128          480   Dictyonema         <NA>          <NA>          <NA>
    ## 1137          480   Dictyonema         <NA>          <NA>          <NA>
    ## 1168          480   Dictyonema         <NA>          <NA>          <NA>
    ## 1246          481   Dictyonema         <NA>          <NA>          <NA>
    ## 1289          482   Dictyonema         <NA>          <NA>          <NA>
    ## 1300          483   Dictyonema         <NA>          <NA>          <NA>
    ## 1303          482   Dictyonema         <NA>          <NA>          <NA>
    ## 1343          665   Dictyonema         <NA>          <NA>          <NA>
    ## 1344          675   Dictyonema         <NA>          <NA>          <NA>
    ## 1345          675   Dictyonema         <NA>          <NA>          <NA>
    ## 1346          665   Dictyonema         <NA>          <NA>          <NA>
    ## 1347          665   Dictyonema         <NA>          <NA>          <NA>
    ## 1348          675   Dictyonema         <NA>          <NA>          <NA>
    ## 1351          675   Dictyonema         <NA>          <NA>          <NA>
    ## 1377          600   Dictyonema         <NA>          <NA>          <NA>
    ## 1382          600   Dictyonema         <NA>          <NA>          <NA>
    ## 1395          663   Dictyonema         <NA>          <NA>          <NA>
    ## 1451          604   Dictyonema         <NA>          <NA>          <NA>
    ## 1455          609   Dictyonema         <NA>          <NA>          <NA>
    ## 1492         4053   Dictyonema         <NA>          <NA>          <NA>
    ## 1536         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1537         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1538         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1539         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1546         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1547         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1548         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1551         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1552         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 1562         4294   Dictyonema         <NA>          <NA>          <NA>
    ## 1784         6165   Dictyonema         <NA>          <NA>          <NA>
    ## 1791         6165   Dictyonema         <NA>          <NA>          <NA>
    ## 1974         6185   Dictyonema         <NA>          <NA>          <NA>
    ## 1981         6189   Dictyonema         <NA>          <NA>          <NA>
    ## 2030         6257   Dictyonema         <NA>    Dictyonema          <NA>
    ## 2045         4261   Dictyonema         <NA>          <NA>          <NA>
    ## 2091          521   Dictyonema         <NA>          <NA>          <NA>
    ## 2095          521   Dictyonema         <NA>          <NA>          <NA>
    ## 2097          521   Dictyonema         <NA>          <NA>          <NA>
    ## 2105          521   Dictyonema         <NA>          <NA>          <NA>
    ## 2109          521   Dictyonema         <NA>          <NA>          <NA>
    ## 2269          676   Dictyonema         <NA>          <NA>          <NA>
    ## 2271          676   Dictyonema         <NA>          <NA>          <NA>
    ## 2273          676   Dictyonema         <NA>          <NA>          <NA>
    ## 2275          677   Dictyonema         <NA>          <NA>          <NA>
    ## 2277          678   Dictyonema         <NA>          <NA>          <NA>
    ## 2280         3861   Dictyonema         <NA>          <NA>          <NA>
    ## 2283         3861   Dictyonema         <NA>          <NA>          <NA>
    ## 2297         6478   Dictyonema         <NA>          <NA>          <NA>
    ## 2302         6478   Dictyonema         <NA>          <NA>          <NA>
    ## 2308         6478   Dictyonema         <NA>          <NA>          <NA>
    ## 2396         6767   Dictyonema         <NA>          <NA>          <NA>
    ## 2397         6767   Dictyonema         <NA>          <NA>          <NA>
    ## 2438         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 2439         4216   Dictyonema         <NA>          <NA>          <NA>
    ## 2487         6922   Dictyonema         <NA>          <NA>          <NA>
    ## 2635         6346   Dictyonema         <NA>          <NA>          <NA>
    ## 2639         6346   Dictyonema         <NA>          <NA>          <NA>
    ## 2673         6376   Dictyonema         <NA>          <NA>          <NA>
    ## 2684         6398   Dictyonema         <NA>          <NA>          <NA>
    ## 2829         4379   Dictyonema         <NA>          <NA>          <NA>
    ## 2833         4379   Dictyonema         <NA>          <NA>          <NA>
    ## 2834         4379   Dictyonema         <NA>          <NA>          <NA>
    ## 2835         4379   Dictyonema         <NA>          <NA>          <NA>
    ## 2840         4294   Dictyonema         <NA>          <NA>          <NA>
    ## 2847         4261   Dictyonema         <NA>          <NA>          <NA>
    ## 3098         7624   Dictyonema         <NA>          <NA>          <NA>
    ## 3118         7624   Dictyonema         <NA>          <NA>          <NA>
    ## 3334         7624   Dictyonema         <NA>          <NA>          <NA>
    ## 3393         7624   Dictyonema         <NA>          <NA>          <NA>
    ## 3400         7624   Dictyonema         <NA>          <NA>          <NA>
    ## 3536        13229   Dictyonema         <NA>          <NA>          <NA>
    ## 3629        18179   Dictyonema         <NA>          <NA>          <NA>
    ## 3666        18179   Dictyonema         <NA>          <NA>          <NA>
    ## 4028        19035   Dictyonema         <NA>          <NA>          <NA>
    ## 4029        19035   Dictyonema         <NA>          <NA>          <NA>
    ## 4030        19035   Dictyonema         <NA>          <NA>          <NA>
    ## 4031        19035   Dictyonema         <NA>          <NA>          <NA>
    ## 4033        16152   Dictyonema         <NA>          <NA>          <NA>
    ## 4036          604   Dictyonema         <NA>          <NA>          <NA>
    ## 4037        24458   Dictyonema         <NA>          <NA>          <NA>
    ## 4052        25447   Dictyonema         <NA>          <NA>          <NA>
    ## 4083        25865   Dictyonema         <NA>          <NA>          <NA>
    ## 4084        25865   Dictyonema         <NA>          <NA>          <NA>
    ## 4085        25865   Dictyonema         <NA>          <NA>          <NA>
    ## 4119        26081   Dictyonema         <NA>          <NA>          <NA>
    ## 4122        26081   Dictyonema         <NA>          <NA>          <NA>
    ## 4126        26081   Dictyonema         <NA>          <NA>          <NA>
    ## 4129        26081   Dictyonema         <NA>          <NA>          <NA>
    ## 4133        26081   Dictyonema         <NA>          <NA>          <NA>
    ## 4154        26333   Dictyonema         <NA>          <NA>          <NA>
    ## 4172        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4173        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4177        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4178        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4179        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4182        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4187        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4189        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4190        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4191        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4192        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4195        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4196        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4199        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4200        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4201        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4204        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4205        27610   Dictyonema         <NA>          <NA>          <NA>
    ## 4241        25414   Dictyonema         <NA>          <NA>          <NA>
    ## 4242        25414   Dictyonema         <NA>          <NA>          <NA>
    ## 4245        25414   Dictyonema         <NA>          <NA>          <NA>
    ## 4246        25414   Dictyonema         <NA>          <NA>          <NA>
    ## 4251        25414   Dictyonema         <NA>          <NA>          <NA>
    ## 4294        18329   Dictyonema         <NA>          <NA>          <NA>
    ## 4295        18329   Dictyonema         <NA>          <NA>          <NA>
    ## 4300        35330   Dictyonema         <NA>          <NA>          <NA>
    ## 4499        37212   Dictyonema         <NA>          <NA>          <NA>
    ## 4511        37504   Dictyonema         <NA>          <NA>          <NA>
    ## 4544          677   Dictyonema         <NA>          <NA>          <NA>
    ## 4547          677   Dictyonema         <NA>          <NA>          <NA>
    ## 5854        50378   Dictyonema         <NA>          <NA>          <NA>
    ## 5855        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5856        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5857        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5858        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5859        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5860        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5861        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5862        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5863        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5864        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5865        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5866        51413   Dictyonema         <NA>          <NA>          <NA>
    ## 5867        51413   Dictyonema         <NA>          <NA>          <NA>
    ##           species_name species_reso subgenus subgenus_no      genus
    ## 8                  sp.         <NA>       NA          NA Dictyonema
    ## 9                  sp.         <NA>       NA          NA Dictyonema
    ## 11                 sp.         <NA>       NA          NA Dictyonema
    ## 15       flabelliforme         <NA>       NA          NA Dictyonema
    ## 21                 sp.         <NA>       NA          NA Dictyonema
    ## 29                 sp.         <NA>       NA          NA Dictyonema
    ## 36                 sp.         <NA>       NA          NA Dictyonema
    ## 118                sp.         <NA>       NA          NA Dictyonema
    ## 136                sp.         <NA>       NA          NA Dictyonema
    ## 139                sp.         <NA>       NA          NA Dictyonema
    ## 141                sp.         <NA>       NA          NA Dictyonema
    ## 176                sp.         <NA>       NA          NA Dictyonema
    ## 199                sp.         <NA>       NA          NA Dictyonema
    ## 202                sp.         <NA>       NA          NA Dictyonema
    ## 384                sp.         <NA>       NA          NA Dictyonema
    ## 387      flabelliforme         <NA>       NA          NA Dictyonema
    ## 390                sp.         <NA>       NA          NA Dictyonema
    ## 434        hamiltoniae         <NA>       NA          NA Dictyonema
    ## 453                sp.         <NA>       NA          NA Dictyonema
    ## 460                sp.         <NA>       NA          NA Dictyonema
    ## 466                sp.         <NA>       NA          NA Dictyonema
    ## 606                sp.         <NA>       NA          NA Dictyonema
    ## 617                sp.         <NA>       NA          NA Dictyonema
    ## 620                sp.         <NA>       NA          NA Dictyonema
    ## 621                sp.         <NA>       NA          NA Dictyonema
    ## 622                sp.         <NA>       NA          NA Dictyonema
    ## 718                sp.         <NA>       NA          NA Dictyonema
    ## 757                sp.         <NA>       NA          NA Dictyonema
    ## 761                sp.         <NA>       NA          NA Dictyonema
    ## 784                sp.         <NA>       NA          NA Dictyonema
    ## 785                sp.         <NA>       NA          NA Dictyonema
    ## 786                sp.         <NA>       NA          NA Dictyonema
    ## 788                sp.         <NA>       NA          NA Dictyonema
    ## 789                sp.         <NA>       NA          NA Dictyonema
    ## 790                sp.         <NA>       NA          NA Dictyonema
    ## 807                sp.         <NA>       NA          NA Dictyonema
    ## 836                sp.         <NA>       NA          NA Dictyonema
    ## 884                sp.         <NA>       NA          NA Dictyonema
    ## 913                sp.         <NA>       NA          NA Dictyonema
    ## 916                sp.         <NA>       NA          NA Dictyonema
    ## 947                sp.         <NA>       NA          NA Dictyonema
    ## 957                sp.         <NA>       NA          NA Dictyonema
    ## 977                sp.         <NA>       NA          NA Dictyonema
    ## 985                sp.         <NA>       NA          NA Dictyonema
    ## 987                sp.         <NA>       NA          NA Dictyonema
    ## 990                sp.         <NA>       NA          NA Dictyonema
    ## 1052               sp.         <NA>       NA          NA Dictyonema
    ## 1128               sp.         <NA>       NA          NA Dictyonema
    ## 1137               sp.         <NA>       NA          NA Dictyonema
    ## 1168               sp.         <NA>       NA          NA Dictyonema
    ## 1246               sp.         <NA>       NA          NA Dictyonema
    ## 1289               sp.         <NA>       NA          NA Dictyonema
    ## 1300               sp.         <NA>       NA          NA Dictyonema
    ## 1303               sp.         <NA>       NA          NA Dictyonema
    ## 1343               sp.         <NA>       NA          NA Dictyonema
    ## 1344               sp.         <NA>       NA          NA Dictyonema
    ## 1345               sp.         <NA>       NA          NA Dictyonema
    ## 1346               sp.         <NA>       NA          NA Dictyonema
    ## 1347               sp.         <NA>       NA          NA Dictyonema
    ## 1348               sp.         <NA>       NA          NA Dictyonema
    ## 1351               sp.         <NA>       NA          NA Dictyonema
    ## 1377               sp.         <NA>       NA          NA Dictyonema
    ## 1382               sp.         <NA>       NA          NA Dictyonema
    ## 1395               sp.         <NA>       NA          NA Dictyonema
    ## 1451     flabelliforme         <NA>       NA          NA Dictyonema
    ## 1455               sp.         <NA>       NA          NA Dictyonema
    ## 1492               sp.         <NA>       NA          NA Dictyonema
    ## 1536         elongatum         <NA>       NA          NA Dictyonema
    ## 1537       subregulare         <NA>       NA          NA Dictyonema
    ## 1538           subtile         <NA>       NA          NA Dictyonema
    ## 1539      crassibasale          cf.       NA          NA Dictyonema
    ## 1546          pragense         <NA>       NA          NA Dictyonema
    ## 1547         goepperti         <NA>       NA          NA Dictyonema
    ## 1548               sp.         <NA>       NA          NA Dictyonema
    ## 1551          pragense         <NA>       NA          NA Dictyonema
    ## 1552         goepperti         <NA>       NA          NA Dictyonema
    ## 1562               sp.         <NA>       NA          NA Dictyonema
    ## 1784         elongatum         <NA>       NA          NA Dictyonema
    ## 1791               sp.         <NA>       NA          NA Dictyonema
    ## 1974      hyskovicense         <NA>       NA          NA Dictyonema
    ## 1981               sp.         <NA>       NA          NA Dictyonema
    ## 2030         elongatum         <NA>       NA          NA Dictyonema
    ## 2045               sp.         <NA>       NA          NA Dictyonema
    ## 2091               sp.         <NA>       NA          NA Dictyonema
    ## 2095               sp.         <NA>       NA          NA Dictyonema
    ## 2097               sp.         <NA>       NA          NA Dictyonema
    ## 2105               sp.         <NA>       NA          NA Dictyonema
    ## 2109               sp.         <NA>       NA          NA Dictyonema
    ## 2269               sp.         <NA>       NA          NA Dictyonema
    ## 2271               sp.         <NA>       NA          NA Dictyonema
    ## 2273               sp.         <NA>       NA          NA Dictyonema
    ## 2275               sp.         <NA>       NA          NA Dictyonema
    ## 2277               sp.         <NA>       NA          NA Dictyonema
    ## 2280               sp.         <NA>       NA          NA Dictyonema
    ## 2283               sp.         <NA>       NA          NA Dictyonema
    ## 2297               sp.         <NA>       NA          NA Dictyonema
    ## 2302               sp.         <NA>       NA          NA Dictyonema
    ## 2308               sp.         <NA>       NA          NA Dictyonema
    ## 2396        francesiae         <NA>       NA          NA Dictyonema
    ## 2397 rockcrossingensis         <NA>       NA          NA Dictyonema
    ## 2438               sp.         <NA>       NA          NA Dictyonema
    ## 2439               sp.         <NA>       NA          NA Dictyonema
    ## 2487               sp.         <NA>       NA          NA Dictyonema
    ## 2635               sp.         <NA>       NA          NA Dictyonema
    ## 2639               sp.         <NA>       NA          NA Dictyonema
    ## 2673               sp.         <NA>       NA          NA Dictyonema
    ## 2684               sp.         <NA>       NA          NA Dictyonema
    ## 2829               sp.         <NA>       NA          NA Dictyonema
    ## 2833         retiforme         <NA>       NA          NA Dictyonema
    ## 2834               sp.         <NA>       NA          NA Dictyonema
    ## 2835               sp.         <NA>       NA          NA Dictyonema
    ## 2840               sp.         <NA>       NA          NA Dictyonema
    ## 2847               sp.         <NA>       NA          NA Dictyonema
    ## 3098               sp.         <NA>       NA          NA Dictyonema
    ## 3118               sp.         <NA>       NA          NA Dictyonema
    ## 3334               sp.         <NA>       NA          NA Dictyonema
    ## 3393               sp.         <NA>       NA          NA Dictyonema
    ## 3400         desmoides          cf.       NA          NA Dictyonema
    ## 3536               sp.         <NA>       NA          NA Dictyonema
    ## 3629        pulchellum         <NA>       NA          NA Dictyonema
    ## 3666        pulchellum         <NA>       NA          NA Dictyonema
    ## 4028             sp. A     informal       NA          NA Dictyonema
    ## 4029             sp. B     informal       NA          NA Dictyonema
    ## 4030             sp. C     informal       NA          NA Dictyonema
    ## 4031             sp. D     informal       NA          NA Dictyonema
    ## 4033      sp. undet. 1     informal       NA          NA Dictyonema
    ## 4036               sp.         <NA>       NA          NA Dictyonema
    ## 4037               sp.         <NA>       NA          NA Dictyonema
    ## 4052               sp.         <NA>       NA          NA Dictyonema
    ## 4083      crassibasale         <NA>       NA          NA Dictyonema
    ## 4084         retiforme         <NA>       NA          NA Dictyonema
    ## 4085          tenellum         <NA>       NA          NA Dictyonema
    ## 4119               sp.         <NA>       NA          NA Dictyonema
    ## 4122          gracilis         <NA>       NA          NA Dictyonema
    ## 4126          gracilis         <NA>       NA          NA Dictyonema
    ## 4129          gracilis         <NA>       NA          NA Dictyonema
    ## 4133               sp.         <NA>       NA          NA Dictyonema
    ## 4154               sp.         <NA>       NA          NA Dictyonema
    ## 4172         retiforme         <NA>       NA          NA Dictyonema
    ## 4173         retiforme         <NA>       NA          NA Dictyonema
    ## 4177      subretiforme         <NA>       NA          NA Dictyonema
    ## 4178           gracile         <NA>       NA          NA Dictyonema
    ## 4179         retiforme         <NA>       NA          NA Dictyonema
    ## 4182         retiforme         <NA>       NA          NA Dictyonema
    ## 4187      subretiforme         <NA>       NA          NA Dictyonema
    ## 4189          gracilis         <NA>       NA          NA Dictyonema
    ## 4190          gracilis         <NA>       NA          NA Dictyonema
    ## 4191          gracilis         <NA>       NA          NA Dictyonema
    ## 4192         retiforme         <NA>       NA          NA Dictyonema
    ## 4195          gracilis         <NA>       NA          NA Dictyonema
    ## 4196         retiforme         <NA>       NA          NA Dictyonema
    ## 4199         retiforme         <NA>       NA          NA Dictyonema
    ## 4200          gracilis         <NA>       NA          NA Dictyonema
    ## 4201         retiforme         <NA>       NA          NA Dictyonema
    ## 4204          gracilis         <NA>       NA          NA Dictyonema
    ## 4205         retiforme         <NA>       NA          NA Dictyonema
    ## 4241               sp.         <NA>       NA          NA Dictyonema
    ## 4242     flabelliforme          cf.       NA          NA Dictyonema
    ## 4245     flabelliforme          cf.       NA          NA Dictyonema
    ## 4246     flabelliforme          cf.       NA          NA Dictyonema
    ## 4251               sp.         <NA>       NA          NA Dictyonema
    ## 4294               sp.         <NA>       NA          NA Dictyonema
    ## 4295               sp.         <NA>       NA          NA Dictyonema
    ## 4300     flabelliforme         <NA>       NA          NA Dictyonema
    ## 4499               sp.         <NA>       NA          NA Dictyonema
    ## 4511               sp.         <NA>       NA          NA Dictyonema
    ## 4544     flabelliforme         <NA>       NA          NA Dictyonema
    ## 4547        quebecense         <NA>       NA          NA Dictyonema
    ## 5854               sp.         <NA>       NA          NA Dictyonema
    ## 5855      praeparabola         <NA>       NA          NA Dictyonema
    ## 5856      praeparabola         <NA>       NA          NA Dictyonema
    ## 5857           sociale         <NA>       NA          NA Dictyonema
    ## 5858           sociale         <NA>       NA          NA Dictyonema
    ## 5859          parabola         <NA>       NA          NA Dictyonema
    ## 5860           sociale         <NA>       NA          NA Dictyonema
    ## 5861          parabola         <NA>       NA          NA Dictyonema
    ## 5862           sociale         <NA>       NA          NA Dictyonema
    ## 5863          parabola         <NA>       NA          NA Dictyonema
    ## 5864           sociale         <NA>       NA          NA Dictyonema
    ## 5865          parabola         <NA>       NA          NA Dictyonema
    ## 5866     flabelliforme         <NA>       NA          NA Dictyonema
    ## 5867               sp.         <NA>       NA          NA Dictyonema
    ##      genus_no          family family_no      order order_no         class
    ## 8       33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 9       33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 11      33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 15      33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 21      33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 29      33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 36      33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 118     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 136     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 139     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 141     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 176     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 199     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 202     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 384     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 387     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 390     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 434     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 453     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 460     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 466     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 606     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 617     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 620     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 621     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 622     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 718     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 757     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 761     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 784     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 785     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 786     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 788     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 789     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 790     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 807     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 836     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 884     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 913     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 916     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 947     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 957     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 977     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 985     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 987     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 990     33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1052    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1128    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1137    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1168    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1246    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1289    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1300    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1303    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1343    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1344    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1345    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1346    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1347    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1348    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1351    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1377    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1382    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1395    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1451    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1455    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1492    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1536    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1537    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1538    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1539    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1546    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1547    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1548    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1551    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1552    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1562    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1784    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1791    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1974    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 1981    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2030    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2045    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2091    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2095    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2097    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2105    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2109    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2269    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2271    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2273    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2275    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2277    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2280    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2283    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2297    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2302    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2308    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2396    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2397    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2438    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2439    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2487    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2635    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2639    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2673    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2684    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2829    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2833    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2834    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2835    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2840    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 2847    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3098    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3118    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3334    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3393    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3400    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3536    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3629    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 3666    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4028    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4029    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4030    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4031    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4033    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4036    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4037    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4052    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4083    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4084    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4085    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4119    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4122    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4126    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4129    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4133    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4154    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4172    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4173    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4177    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4178    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4179    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4182    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4187    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4189    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4190    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4191    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4192    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4195    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4196    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4199    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4200    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4201    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4204    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4205    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4241    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4242    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4245    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4246    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4251    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4294    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4295    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4300    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4499    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4511    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4544    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 4547    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5854    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5855    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5856    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5857    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5858    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5859    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5860    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5861    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5862    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5863    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5864    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5865    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5866    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ## 5867    33553 Dendrograptidae     88802 Dendroidea    33535 Graptolithina
    ##      class_no       phylum phylum_no           authorizer
    ## 8       33534 Hemichordata     33518         Sepkoski, J.
    ## 9       33534 Hemichordata     33518         Sepkoski, J.
    ## 11      33534 Hemichordata     33518         Sepkoski, J.
    ## 15      33534 Hemichordata     33518         Sepkoski, J.
    ## 21      33534 Hemichordata     33518         Sepkoski, J.
    ## 29      33534 Hemichordata     33518         Sepkoski, J.
    ## 36      33534 Hemichordata     33518         Sepkoski, J.
    ## 118     33534 Hemichordata     33518         Sepkoski, J.
    ## 136     33534 Hemichordata     33518         Sepkoski, J.
    ## 139     33534 Hemichordata     33518         Sepkoski, J.
    ## 141     33534 Hemichordata     33518         Sepkoski, J.
    ## 176     33534 Hemichordata     33518         Sepkoski, J.
    ## 199     33534 Hemichordata     33518         Sepkoski, J.
    ## 202     33534 Hemichordata     33518         Sepkoski, J.
    ## 384     33534 Hemichordata     33518           Miller, A.
    ## 387     33534 Hemichordata     33518           Miller, A.
    ## 390     33534 Hemichordata     33518           Miller, A.
    ## 434     33534 Hemichordata     33518           Miller, A.
    ## 453     33534 Hemichordata     33518           Miller, A.
    ## 460     33534 Hemichordata     33518           Miller, A.
    ## 466     33534 Hemichordata     33518           Miller, A.
    ## 606     33534 Hemichordata     33518           Miller, A.
    ## 617     33534 Hemichordata     33518           Miller, A.
    ## 620     33534 Hemichordata     33518           Miller, A.
    ## 621     33534 Hemichordata     33518           Miller, A.
    ## 622     33534 Hemichordata     33518           Miller, A.
    ## 718     33534 Hemichordata     33518           Miller, A.
    ## 757     33534 Hemichordata     33518           Miller, A.
    ## 761     33534 Hemichordata     33518           Miller, A.
    ## 784     33534 Hemichordata     33518           Miller, A.
    ## 785     33534 Hemichordata     33518           Miller, A.
    ## 786     33534 Hemichordata     33518           Miller, A.
    ## 788     33534 Hemichordata     33518           Miller, A.
    ## 789     33534 Hemichordata     33518           Miller, A.
    ## 790     33534 Hemichordata     33518           Miller, A.
    ## 807     33534 Hemichordata     33518           Miller, A.
    ## 836     33534 Hemichordata     33518           Miller, A.
    ## 884     33534 Hemichordata     33518           Miller, A.
    ## 913     33534 Hemichordata     33518           Miller, A.
    ## 916     33534 Hemichordata     33518           Miller, A.
    ## 947     33534 Hemichordata     33518           Miller, A.
    ## 957     33534 Hemichordata     33518           Miller, A.
    ## 977     33534 Hemichordata     33518           Miller, A.
    ## 985     33534 Hemichordata     33518           Miller, A.
    ## 987     33534 Hemichordata     33518           Miller, A.
    ## 990     33534 Hemichordata     33518           Miller, A.
    ## 1052    33534 Hemichordata     33518           Miller, A.
    ## 1128    33534 Hemichordata     33518           Miller, A.
    ## 1137    33534 Hemichordata     33518           Miller, A.
    ## 1168    33534 Hemichordata     33518           Miller, A.
    ## 1246    33534 Hemichordata     33518           Miller, A.
    ## 1289    33534 Hemichordata     33518           Miller, A.
    ## 1300    33534 Hemichordata     33518           Miller, A.
    ## 1303    33534 Hemichordata     33518           Miller, A.
    ## 1343    33534 Hemichordata     33518           Miller, A.
    ## 1344    33534 Hemichordata     33518           Miller, A.
    ## 1345    33534 Hemichordata     33518           Miller, A.
    ## 1346    33534 Hemichordata     33518           Miller, A.
    ## 1347    33534 Hemichordata     33518           Miller, A.
    ## 1348    33534 Hemichordata     33518           Miller, A.
    ## 1351    33534 Hemichordata     33518           Miller, A.
    ## 1377    33534 Hemichordata     33518           Miller, A.
    ## 1382    33534 Hemichordata     33518           Miller, A.
    ## 1395    33534 Hemichordata     33518           Miller, A.
    ## 1451    33534 Hemichordata     33518           Miller, A.
    ## 1455    33534 Hemichordata     33518           Miller, A.
    ## 1492    33534 Hemichordata     33518           Gensel, P.
    ## 1536    33534 Hemichordata     33518           Miller, A.
    ## 1537    33534 Hemichordata     33518           Miller, A.
    ## 1538    33534 Hemichordata     33518           Miller, A.
    ## 1539    33534 Hemichordata     33518           Miller, A.
    ## 1546    33534 Hemichordata     33518           Miller, A.
    ## 1547    33534 Hemichordata     33518           Miller, A.
    ## 1548    33534 Hemichordata     33518           Miller, A.
    ## 1551    33534 Hemichordata     33518           Miller, A.
    ## 1552    33534 Hemichordata     33518           Miller, A.
    ## 1562    33534 Hemichordata     33518            Foote, M.
    ## 1784    33534 Hemichordata     33518            Foote, M.
    ## 1791    33534 Hemichordata     33518            Foote, M.
    ## 1974    33534 Hemichordata     33518            Foote, M.
    ## 1981    33534 Hemichordata     33518            Foote, M.
    ## 2030    33534 Hemichordata     33518            Foote, M.
    ## 2045    33534 Hemichordata     33518            Foote, M.
    ## 2091    33534 Hemichordata     33518           Miller, A.
    ## 2095    33534 Hemichordata     33518           Miller, A.
    ## 2097    33534 Hemichordata     33518           Miller, A.
    ## 2105    33534 Hemichordata     33518           Miller, A.
    ## 2109    33534 Hemichordata     33518           Miller, A.
    ## 2269    33534 Hemichordata     33518           Miller, A.
    ## 2271    33534 Hemichordata     33518           Miller, A.
    ## 2273    33534 Hemichordata     33518           Miller, A.
    ## 2275    33534 Hemichordata     33518           Miller, A.
    ## 2277    33534 Hemichordata     33518           Miller, A.
    ## 2280    33534 Hemichordata     33518           Miller, A.
    ## 2283    33534 Hemichordata     33518           Miller, A.
    ## 2297    33534 Hemichordata     33518           Miller, A.
    ## 2302    33534 Hemichordata     33518           Miller, A.
    ## 2308    33534 Hemichordata     33518           Miller, A.
    ## 2396    33534 Hemichordata     33518          Holland, S.
    ## 2397    33534 Hemichordata     33518          Holland, S.
    ## 2438    33534 Hemichordata     33518           Miller, A.
    ## 2439    33534 Hemichordata     33518           Miller, A.
    ## 2487    33534 Hemichordata     33518          Holland, S.
    ## 2635    33534 Hemichordata     33518           Miller, A.
    ## 2639    33534 Hemichordata     33518           Miller, A.
    ## 2673    33534 Hemichordata     33518           Miller, A.
    ## 2684    33534 Hemichordata     33518           Miller, A.
    ## 2829    33534 Hemichordata     33518            Foote, M.
    ## 2833    33534 Hemichordata     33518            Foote, M.
    ## 2834    33534 Hemichordata     33518            Foote, M.
    ## 2835    33534 Hemichordata     33518            Foote, M.
    ## 2840    33534 Hemichordata     33518            Foote, M.
    ## 2847    33534 Hemichordata     33518            Foote, M.
    ## 3098    33534 Hemichordata     33518            Foote, M.
    ## 3118    33534 Hemichordata     33518            Foote, M.
    ## 3334    33534 Hemichordata     33518            Foote, M.
    ## 3393    33534 Hemichordata     33518            Foote, M.
    ## 3400    33534 Hemichordata     33518            Foote, M.
    ## 3536    33534 Hemichordata     33518            Hendy, A.
    ## 3629    33534 Hemichordata     33518            Hendy, A.
    ## 3666    33534 Hemichordata     33518            Hendy, A.
    ## 4028    33534 Hemichordata     33518        Kiessling, W.
    ## 4029    33534 Hemichordata     33518        Kiessling, W.
    ## 4030    33534 Hemichordata     33518        Kiessling, W.
    ## 4031    33534 Hemichordata     33518        Kiessling, W.
    ## 4033    33534 Hemichordata     33518           Wagner, P.
    ## 4036    33534 Hemichordata     33518           Miller, A.
    ## 4037    33534 Hemichordata     33518        Kiessling, W.
    ## 4052    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4083    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4084    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4085    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4119    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4122    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4126    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4129    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4133    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4154    33534 Hemichordata     33518        Kiessling, W.
    ## 4172    33534 Hemichordata     33518            Ivany, L.
    ## 4173    33534 Hemichordata     33518            Ivany, L.
    ## 4177    33534 Hemichordata     33518            Ivany, L.
    ## 4178    33534 Hemichordata     33518            Ivany, L.
    ## 4179    33534 Hemichordata     33518            Ivany, L.
    ## 4182    33534 Hemichordata     33518            Ivany, L.
    ## 4187    33534 Hemichordata     33518            Ivany, L.
    ## 4189    33534 Hemichordata     33518            Ivany, L.
    ## 4190    33534 Hemichordata     33518            Ivany, L.
    ## 4191    33534 Hemichordata     33518            Ivany, L.
    ## 4192    33534 Hemichordata     33518            Ivany, L.
    ## 4195    33534 Hemichordata     33518            Ivany, L.
    ## 4196    33534 Hemichordata     33518            Ivany, L.
    ## 4199    33534 Hemichordata     33518            Ivany, L.
    ## 4200    33534 Hemichordata     33518            Ivany, L.
    ## 4201    33534 Hemichordata     33518            Ivany, L.
    ## 4204    33534 Hemichordata     33518            Ivany, L.
    ## 4205    33534 Hemichordata     33518            Ivany, L.
    ## 4241    33534 Hemichordata     33518          Hopkins, M.
    ## 4242    33534 Hemichordata     33518          Hopkins, M.
    ## 4245    33534 Hemichordata     33518          Hopkins, M.
    ## 4246    33534 Hemichordata     33518          Hopkins, M.
    ## 4251    33534 Hemichordata     33518          Hopkins, M.
    ## 4294    33534 Hemichordata     33518         Finnegan, S.
    ## 4295    33534 Hemichordata     33518         Finnegan, S.
    ## 4300    33534 Hemichordata     33518          Hopkins, M.
    ## 4499    33534 Hemichordata     33518           Miller, A.
    ## 4511    33534 Hemichordata     33518           Miller, A.
    ## 4544    33534 Hemichordata     33518        Kiessling, W.
    ## 4547    33534 Hemichordata     33518        Kiessling, W.
    ## 5854    33534 Hemichordata     33518        Kiessling, W.
    ## 5855    33534 Hemichordata     33518          Hopkins, M.
    ## 5856    33534 Hemichordata     33518          Hopkins, M.
    ## 5857    33534 Hemichordata     33518          Hopkins, M.
    ## 5858    33534 Hemichordata     33518          Hopkins, M.
    ## 5859    33534 Hemichordata     33518          Hopkins, M.
    ## 5860    33534 Hemichordata     33518          Hopkins, M.
    ## 5861    33534 Hemichordata     33518          Hopkins, M.
    ## 5862    33534 Hemichordata     33518          Hopkins, M.
    ## 5863    33534 Hemichordata     33518          Hopkins, M.
    ## 5864    33534 Hemichordata     33518          Hopkins, M.
    ## 5865    33534 Hemichordata     33518          Hopkins, M.
    ## 5866    33534 Hemichordata     33518          Hopkins, M.
    ## 5867    33534 Hemichordata     33518          Hopkins, M.
    ##                   enterer             modifier
    ## 8             Sommers, M.              unknown
    ## 9             Sommers, M.              unknown
    ## 11            Sommers, M.              unknown
    ## 15            Sommers, M.              unknown
    ## 21            Sommers, M.           Wagner, P.
    ## 29            Sommers, M.              unknown
    ## 36            Sommers, M.              unknown
    ## 118           Sommers, M.              unknown
    ## 136           Sommers, M.              unknown
    ## 139           Sommers, M.              unknown
    ## 141           Sommers, M.              unknown
    ## 176           Sommers, M.              unknown
    ## 199           Sommers, M.              unknown
    ## 202           Sommers, M.              unknown
    ## 384  Novack-Gottshall, P.              unknown
    ## 387  Novack-Gottshall, P.              unknown
    ## 390  Novack-Gottshall, P.              unknown
    ## 434             Layou, K.            Sessa, J.
    ## 453  Novack-Gottshall, P.              unknown
    ## 460  Novack-Gottshall, P.              unknown
    ## 466  Novack-Gottshall, P.              unknown
    ## 606  Novack-Gottshall, P.              unknown
    ## 617  Novack-Gottshall, P.              unknown
    ## 620  Novack-Gottshall, P.              unknown
    ## 621  Novack-Gottshall, P.              unknown
    ## 622  Novack-Gottshall, P.              unknown
    ## 718  Novack-Gottshall, P.              unknown
    ## 757  Novack-Gottshall, P.              unknown
    ## 761  Novack-Gottshall, P.              unknown
    ## 784  Novack-Gottshall, P.              unknown
    ## 785  Novack-Gottshall, P.              unknown
    ## 786  Novack-Gottshall, P.              unknown
    ## 788  Novack-Gottshall, P.              unknown
    ## 789  Novack-Gottshall, P.              unknown
    ## 790  Novack-Gottshall, P.              unknown
    ## 807  Novack-Gottshall, P.              unknown
    ## 836  Novack-Gottshall, P.              unknown
    ## 884  Novack-Gottshall, P.              unknown
    ## 913  Novack-Gottshall, P.              unknown
    ## 916  Novack-Gottshall, P.              unknown
    ## 947  Novack-Gottshall, P.              unknown
    ## 957  Novack-Gottshall, P.              unknown
    ## 977  Novack-Gottshall, P.              unknown
    ## 985  Novack-Gottshall, P.              unknown
    ## 987  Novack-Gottshall, P.              unknown
    ## 990  Novack-Gottshall, P.              unknown
    ## 1052 Novack-Gottshall, P.              unknown
    ## 1128 Novack-Gottshall, P.              unknown
    ## 1137 Novack-Gottshall, P.              unknown
    ## 1168 Novack-Gottshall, P.              unknown
    ## 1246 Novack-Gottshall, P.              unknown
    ## 1289 Novack-Gottshall, P.              unknown
    ## 1300 Novack-Gottshall, P.              unknown
    ## 1303 Novack-Gottshall, P.              unknown
    ## 1343 Novack-Gottshall, P.              unknown
    ## 1344 Novack-Gottshall, P.              unknown
    ## 1345 Novack-Gottshall, P.              unknown
    ## 1346 Novack-Gottshall, P.              unknown
    ## 1347 Novack-Gottshall, P.              unknown
    ## 1348 Novack-Gottshall, P.              unknown
    ## 1351 Novack-Gottshall, P.              unknown
    ## 1377 Novack-Gottshall, P.              unknown
    ## 1382 Novack-Gottshall, P.              unknown
    ## 1395 Novack-Gottshall, P.              unknown
    ## 1451 Novack-Gottshall, P.              unknown
    ## 1455 Novack-Gottshall, P.              unknown
    ## 1492            Kotyk, M.           Gensel, P.
    ## 1536            Sessa, J.              unknown
    ## 1537            Sessa, J.              unknown
    ## 1538            Sessa, J.              unknown
    ## 1539            Sessa, J.              unknown
    ## 1546            Sessa, J.              unknown
    ## 1547            Sessa, J.              unknown
    ## 1548            Sessa, J.              unknown
    ## 1551            Sessa, J.              unknown
    ## 1552            Sessa, J.              unknown
    ## 1562         Koverman, K.              unknown
    ## 1784            Foote, M.              unknown
    ## 1791            Foote, M.              unknown
    ## 1974            Foote, M.              unknown
    ## 1981            Foote, M.              unknown
    ## 2030            Foote, M.              unknown
    ## 2045            Foote, M.              unknown
    ## 2091 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2095 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2097 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2105 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2109 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2269 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2271 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2273 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2275 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2277 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2280 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2283 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2297 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2302 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2308 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2396           Hanson, T.              unknown
    ## 2397           Hanson, T.              unknown
    ## 2438            Sessa, J.              unknown
    ## 2439            Sessa, J.              unknown
    ## 2487           Hanson, T.              unknown
    ## 2635 Novack-Gottshall, P.          Villier, L.
    ## 2639 Novack-Gottshall, P.          Villier, L.
    ## 2673 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2684 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2829            Foote, M.              unknown
    ## 2833            Foote, M.              unknown
    ## 2834            Foote, M.              unknown
    ## 2835            Foote, M.           Merkel, U.
    ## 2840            Foote, M.              unknown
    ## 2847            Foote, M.              unknown
    ## 3098            Foote, M.              unknown
    ## 3118            Foote, M.              unknown
    ## 3334            Foote, M.              unknown
    ## 3393            Foote, M.              unknown
    ## 3400            Foote, M.              unknown
    ## 3536            Hendy, A.              unknown
    ## 3629            Hendy, A.            Hendy, A.
    ## 3666            Hendy, A.              unknown
    ## 4028        Kiessling, W.              unknown
    ## 4029        Kiessling, W.              unknown
    ## 4030        Kiessling, W.              unknown
    ## 4031        Kiessling, W.              unknown
    ## 4033           Wagner, P.              unknown
    ## 4036            Sessa, J.              unknown
    ## 4037           Merkel, U.              unknown
    ## 4052            Hearn, P.              unknown
    ## 4083            Hearn, P.              unknown
    ## 4084            Hearn, P.              unknown
    ## 4085            Hearn, P.              unknown
    ## 4119            Hearn, P.              unknown
    ## 4122            Hearn, P.              unknown
    ## 4126            Hearn, P.              unknown
    ## 4129            Hearn, P.              unknown
    ## 4133            Hearn, P.              unknown
    ## 4154           Merkel, U.              unknown
    ## 4172             Wall, P.              unknown
    ## 4173             Wall, P.              unknown
    ## 4177             Wall, P.              unknown
    ## 4178             Wall, P.              unknown
    ## 4179             Wall, P.              unknown
    ## 4182             Wall, P.              unknown
    ## 4187             Wall, P.              unknown
    ## 4189             Wall, P.              unknown
    ## 4190             Wall, P.              unknown
    ## 4191             Wall, P.              unknown
    ## 4192             Wall, P.              unknown
    ## 4195             Wall, P.              unknown
    ## 4196             Wall, P.              unknown
    ## 4199             Wall, P.              unknown
    ## 4200             Wall, P.              unknown
    ## 4201             Wall, P.              unknown
    ## 4204             Wall, P.              unknown
    ## 4205             Wall, P.              unknown
    ## 4241          Hopkins, M.              unknown
    ## 4242          Hopkins, M.              unknown
    ## 4245          Hopkins, M.              unknown
    ## 4246          Hopkins, M.              unknown
    ## 4251          Hopkins, M.              unknown
    ## 4294         Finnegan, S.          Hopkins, M.
    ## 4295         Finnegan, S.          Hopkins, M.
    ## 4300          Hopkins, M.              unknown
    ## 4499            Kolbe, S.              unknown
    ## 4511            Kolbe, S.              unknown
    ## 4544           Merkel, U.              unknown
    ## 4547           Merkel, U.              unknown
    ## 5854           Krause, M.              unknown
    ## 5855          Mahmood, S.              unknown
    ## 5856          Mahmood, S.              unknown
    ## 5857          Mahmood, S.              unknown
    ## 5858          Mahmood, S.              unknown
    ## 5859          Mahmood, S.              unknown
    ## 5860          Mahmood, S.              unknown
    ## 5861          Mahmood, S.              unknown
    ## 5862          Mahmood, S.              unknown
    ## 5863          Mahmood, S.              unknown
    ## 5864          Mahmood, S.              unknown
    ## 5865          Mahmood, S.              unknown
    ## 5866          Mahmood, S.              unknown
    ## 5867          Mahmood, S.              unknown
    ## 
    ## $Dicranograptidae
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 69            3401  occurrence      NA       NA           328
    ## 75            3465  occurrence      NA       NA           331
    ## 78            3790  occurrence      NA       NA           339
    ## 100           4687  occurrence      NA       NA           380
    ## 212          36012  occurrence      NA       NA          2655
    ## 228          38199  occurrence      NA       NA          2709
    ## 265          48735  occurrence      NA       NA          2770
    ## 305          49369  occurrence      NA       NA          2950
    ## 314          49392  occurrence      NA       NA          3179
    ## 419          52188  occurrence      NA       NA          3874
    ## 446         105284  occurrence      NA       NA          2951
    ## 491         105420  occurrence      NA       NA          4667
    ## 495         105424  occurrence      NA       NA          4668
    ## 526         105475  occurrence      NA       NA          4676
    ## 555         105542  occurrence      NA       NA          4685
    ## 589         105794  occurrence      NA       NA          4711
    ## 925         107719  occurrence      NA       NA          7708
    ## 931         107725  occurrence      NA       NA          7709
    ## 935         107729  occurrence      NA       NA          7710
    ## 1014        108071  occurrence      NA       NA          7751
    ## 1141        108387  occurrence      NA       NA          7782
    ## 1176        108427  occurrence      NA       NA          7796
    ## 1254        108590  occurrence      NA       NA          7834
    ## 1312        109309  occurrence      NA       NA          7951
    ## 1328        118180  occurrence      NA       NA          8776
    ## 1363        118502  occurrence      NA       NA          8858
    ## 1434        118759  occurrence      NA       NA          8889
    ## 1440        118792  occurrence      NA       NA          8892
    ## 1467        118973  occurrence      NA       NA          9035
    ## 2121        240571  occurrence      NA       NA          8527
    ## 2126        240576  occurrence      NA       NA          8528
    ## 2152        240656  occurrence      NA       NA          8535
    ## 2175        240848  occurrence      NA       NA          8552
    ## 2180        240856  occurrence      NA       NA          8553
    ## 2216        240984  occurrence      NA       NA          8565
    ## 2267        241126  occurrence      NA       NA          8578
    ## 2290        242117  occurrence      NA       NA         20764
    ## 2315        242351  occurrence      NA       NA         20791
    ## 2334        242393  occurrence      NA       NA         20801
    ## 2359        242488  occurrence      NA       NA         20808
    ## 2378        242534  occurrence      NA       NA         23592
    ## 2386        242558  occurrence      NA       NA         23595
    ## 2422        251852  occurrence      NA       NA         24537
    ## 2563        262274  occurrence      NA       NA         25338
    ## 2589        263702  occurrence      NA       NA         25513
    ## 2595        263716  occurrence      NA       NA         25516
    ## 2611        263800  occurrence      NA       NA         25532
    ## 3472        446192  occurrence      NA       NA          8680
    ## 3478        446215  occurrence      NA       NA          8681
    ## 3480        446234  occurrence      NA       NA          8682
    ## 3547        538659  occurrence      NA       NA         56002
    ## 3841        598664  occurrence      NA       NA         63445
    ## 3918        601835  occurrence      NA       NA         63956
    ## 4098        715625  occurrence      NA       NA         76748
    ## 4103        715640  occurrence      NA       NA         76751
    ## 4108        716402  occurrence      NA       NA         76902
    ## 4228        882627  occurrence      NA       NA         13513
    ## 4330        955101  occurrence      NA       NA        111713
    ## 4418        969189  occurrence      NA       NA        114852
    ## 4660       1139684  occurrence      NA       NA        145227
    ## 4680       1139705  occurrence      NA       NA        145233
    ## 4681       1139706  occurrence      NA       NA        145233
    ## 4690       1139726  occurrence      NA       NA        145236
    ## 4693       1139729  occurrence      NA       NA        145236
    ## 4699       1139737  occurrence      NA       NA        145237
    ## 4700       1139738  occurrence      NA       NA        145237
    ## 4707       1139745  occurrence      NA       NA        145238
    ## 4708       1139746  occurrence      NA       NA        145238
    ## 4717       1139755  occurrence      NA       NA        145239
    ## 4721       1139759  occurrence      NA       NA        145240
    ## 4722       1139760  occurrence      NA       NA        145240
    ## 4760       1140649  occurrence      NA       NA        145331
    ## 4769       1141823  occurrence      NA       NA        145464
    ## 5875       1232084  occurrence      NA       NA        162194
    ## 5877       1232104  occurrence      NA       NA        162197
    ## 5879       1232125  occurrence      NA       NA        162198
    ## 5880       1232126  occurrence      NA       NA        162199
    ##                     identified_name identified_rank identified_no
    ## 69               Dicranograptus sp.           genus         33653
    ## 75               Dicranograptus sp.           genus         33653
    ## 78               Dicranograptus sp.           genus         33653
    ## 100              Dicranograptus sp.           genus         33653
    ## 212              Dicranograptus sp.           genus         33653
    ## 228              Dicranograptus sp.           genus         33653
    ## 265              Dicranograptus sp.           genus         33653
    ## 305              Dicranograptus sp.           genus         33653
    ## 314              Dicranograptus sp.           genus         33653
    ## 419              Dicranograptus sp.           genus         33653
    ## 446              Dicranograptus sp.           genus         33653
    ## 491              Dicranograptus sp.           genus         33653
    ## 495              Dicranograptus sp.           genus         33653
    ## 526              Dicranograptus sp.           genus         33653
    ## 555              Dicranograptus sp.           genus         33653
    ## 589              Dicranograptus sp.           genus         33653
    ## 925              Dicranograptus sp.           genus         33653
    ## 931              Dicranograptus sp.           genus         33653
    ## 935              Dicranograptus sp.           genus         33653
    ## 1014             Dicranograptus sp.           genus         33653
    ## 1141             Dicranograptus sp.           genus         33653
    ## 1176             Dicranograptus sp.           genus         33653
    ## 1254             Dicranograptus sp.           genus         33653
    ## 1312             Dicranograptus sp.           genus         33653
    ## 1328             Dicranograptus sp.           genus         33653
    ## 1363             Dicranograptus sp.           genus         33653
    ## 1434             Dicranograptus sp.           genus         33653
    ## 1440             Dicranograptus sp.           genus         33653
    ## 1467             Dicranograptus sp.           genus         33653
    ## 2121             Dicranograptus sp.           genus         33653
    ## 2126             Dicranograptus sp.           genus         33653
    ## 2152             Dicranograptus sp.           genus         33653
    ## 2175             Dicranograptus sp.           genus         33653
    ## 2180             Dicranograptus sp.           genus         33653
    ## 2216             Dicranograptus sp.           genus         33653
    ## 2267             Dicranograptus sp.           genus         33653
    ## 2290             Dicranograptus sp.           genus         33653
    ## 2315             Dicranograptus sp.           genus         33653
    ## 2334             Dicranograptus sp.           genus         33653
    ## 2359             Dicranograptus sp.           genus         33653
    ## 2378             Dicranograptus sp.           genus         33653
    ## 2386             Dicranograptus sp.           genus         33653
    ## 2422     Dicranograptus brevicaulis         species         33653
    ## 2563             Dicranograptus sp.           genus         33653
    ## 2589             Dicranograptus sp.           genus         33653
    ## 2595             Dicranograptus sp.           genus         33653
    ## 2611             Dicranograptus sp.           genus         33653
    ## 3472             Dicranograptus sp.           genus         33653
    ## 3478             Dicranograptus sp.           genus         33653
    ## 3480             Dicranograptus sp.           genus         33653
    ## 3547             Dicranograptus sp.           genus         33653
    ## 3841      Dicranograptus nicholsoni         species         33653
    ## 3918      Dicranograptus nicholsoni         species         33653
    ## 4098      Dicranograptus nicholsoni         species         33653
    ## 4103      Dicranograptus nicholsoni         species         33653
    ## 4108        Dicranograptus clingani         species         33653
    ## 4228    Dicranograptus ramosus aff.         species        306404
    ## 4330             Dicranograptus sp.           genus         33653
    ## 4418     Dicranograptus contortus ?         species         33653
    ## 4660 Dicranograptus brevicaulis cf.         species         33653
    ## 4680       Dicranograptus contortus         species         33653
    ## 4681    Dicranograptus spinifer cf.         species         33653
    ## 4690       Dicranograptus contortus         species         33653
    ## 4693      Dicranograptus nicholsoni         species         33653
    ## 4699       Dicranograptus contortus         species         33653
    ## 4700      Dicranograptus nicholsoni         species         33653
    ## 4707       Dicranograptus contortus         species         33653
    ## 4708      Dicranograptus nicholsoni         species         33653
    ## 4717      Dicranograptus nicholsoni         species         33653
    ## 4721       Dicranograptus kirki cf.         species         33653
    ## 4722        Dicranograptus spinifer         species         33653
    ## 4760 Dicranograptus brevicaulis cf.         species         33653
    ## 4769       Dicranograptus kirki cf.         species         33653
    ## 5875         Dicranograptus ramosus         species        306404
    ## 5877           Dicranograptus hians         species         33653
    ## 5879           Dicranograptus hians         species         33653
    ## 5880           Dicranograptus hians         species         33653
    ##             taxonomic_reason          accepted_name accepted_rank
    ## 69                      <NA>         Dicranograptus         genus
    ## 75                      <NA>         Dicranograptus         genus
    ## 78                      <NA>         Dicranograptus         genus
    ## 100                     <NA>         Dicranograptus         genus
    ## 212                     <NA>         Dicranograptus         genus
    ## 228                     <NA>         Dicranograptus         genus
    ## 265                     <NA>         Dicranograptus         genus
    ## 305                     <NA>         Dicranograptus         genus
    ## 314                     <NA>         Dicranograptus         genus
    ## 419                     <NA>         Dicranograptus         genus
    ## 446                     <NA>         Dicranograptus         genus
    ## 491                     <NA>         Dicranograptus         genus
    ## 495                     <NA>         Dicranograptus         genus
    ## 526                     <NA>         Dicranograptus         genus
    ## 555                     <NA>         Dicranograptus         genus
    ## 589                     <NA>         Dicranograptus         genus
    ## 925                     <NA>         Dicranograptus         genus
    ## 931                     <NA>         Dicranograptus         genus
    ## 935                     <NA>         Dicranograptus         genus
    ## 1014                    <NA>         Dicranograptus         genus
    ## 1141                    <NA>         Dicranograptus         genus
    ## 1176                    <NA>         Dicranograptus         genus
    ## 1254                    <NA>         Dicranograptus         genus
    ## 1312                    <NA>         Dicranograptus         genus
    ## 1328                    <NA>         Dicranograptus         genus
    ## 1363                    <NA>         Dicranograptus         genus
    ## 1434                    <NA>         Dicranograptus         genus
    ## 1440                    <NA>         Dicranograptus         genus
    ## 1467                    <NA>         Dicranograptus         genus
    ## 2121                    <NA>         Dicranograptus         genus
    ## 2126                    <NA>         Dicranograptus         genus
    ## 2152                    <NA>         Dicranograptus         genus
    ## 2175                    <NA>         Dicranograptus         genus
    ## 2180                    <NA>         Dicranograptus         genus
    ## 2216                    <NA>         Dicranograptus         genus
    ## 2267                    <NA>         Dicranograptus         genus
    ## 2290                    <NA>         Dicranograptus         genus
    ## 2315                    <NA>         Dicranograptus         genus
    ## 2334                    <NA>         Dicranograptus         genus
    ## 2359                    <NA>         Dicranograptus         genus
    ## 2378                    <NA>         Dicranograptus         genus
    ## 2386                    <NA>         Dicranograptus         genus
    ## 2422 taxon not fully entered         Dicranograptus         genus
    ## 2563                    <NA>         Dicranograptus         genus
    ## 2589                    <NA>         Dicranograptus         genus
    ## 2595                    <NA>         Dicranograptus         genus
    ## 2611                    <NA>         Dicranograptus         genus
    ## 3472                    <NA>         Dicranograptus         genus
    ## 3478                    <NA>         Dicranograptus         genus
    ## 3480                    <NA>         Dicranograptus         genus
    ## 3547                    <NA>         Dicranograptus         genus
    ## 3841 taxon not fully entered         Dicranograptus         genus
    ## 3918 taxon not fully entered         Dicranograptus         genus
    ## 4098 taxon not fully entered         Dicranograptus         genus
    ## 4103 taxon not fully entered         Dicranograptus         genus
    ## 4108 taxon not fully entered         Dicranograptus         genus
    ## 4228                    <NA> Dicranograptus ramosus       species
    ## 4330                    <NA>         Dicranograptus         genus
    ## 4418 taxon not fully entered         Dicranograptus         genus
    ## 4660 taxon not fully entered         Dicranograptus         genus
    ## 4680 taxon not fully entered         Dicranograptus         genus
    ## 4681 taxon not fully entered         Dicranograptus         genus
    ## 4690 taxon not fully entered         Dicranograptus         genus
    ## 4693 taxon not fully entered         Dicranograptus         genus
    ## 4699 taxon not fully entered         Dicranograptus         genus
    ## 4700 taxon not fully entered         Dicranograptus         genus
    ## 4707 taxon not fully entered         Dicranograptus         genus
    ## 4708 taxon not fully entered         Dicranograptus         genus
    ## 4717 taxon not fully entered         Dicranograptus         genus
    ## 4721 taxon not fully entered         Dicranograptus         genus
    ## 4722 taxon not fully entered         Dicranograptus         genus
    ## 4760 taxon not fully entered         Dicranograptus         genus
    ## 4769 taxon not fully entered         Dicranograptus         genus
    ## 5875                    <NA> Dicranograptus ramosus       species
    ## 5877 taxon not fully entered         Dicranograptus         genus
    ## 5879 taxon not fully entered         Dicranograptus         genus
    ## 5880 taxon not fully entered         Dicranograptus         genus
    ##      accepted_no  early_interval   late_interval early_age late_age
    ## 69         33653     Black River     Black River     460.9    457.5
    ## 75         33653     Rocklandian     Rocklandian     460.9    449.5
    ## 78         33653      Ordovician      Ordovician     485.4    443.4
    ## 100        33653         Caradoc         Caradoc     460.9    449.5
    ## 212        33653       Eastonian       Eastonian     456.1    449.5
    ## 228        33653       Eastonian          Onnian     456.1    449.5
    ## 265        33653         Idavere         Idavere     460.9    455.8
    ## 305        33653 Early Llandeilo Early Llandeilo     466.0    460.9
    ## 314        33653   Late Llanvirn   Late Llanvirn     463.5    460.9
    ## 419        33653     Longvillian          Onnian     457.5    449.5
    ## 446        33653 Early Llandeilo Early Llandeilo     466.0    460.9
    ## 491        33653         Caradoc         Caradoc     460.9    449.5
    ## 495        33653         Caradoc         Caradoc     460.9    449.5
    ## 526        33653       Llandeilo       Llandeilo     466.0    449.5
    ## 555        33653       Costonian   Marshbrookian     460.9    452.0
    ## 589        33653 Early Llandeilo Early Llandeilo     466.0    460.9
    ## 925        33653       Rawtheyan       Cautleyan     455.8    445.6
    ## 931        33653       Costonian       Harnagian     460.9    455.8
    ## 935        33653       Llandeilo       Llandeilo     466.0    449.5
    ## 1014       33653       Costonian       Harnagian     460.9    455.8
    ## 1141       33653       Llandeilo       Llandeilo     466.0    449.5
    ## 1176       33653       Llandeilo       Llandeilo     466.0    449.5
    ## 1254       33653       Rawtheyan          Wufeng     455.8    443.7
    ## 1312       33653        Llanvirn        Llanvirn     466.0    460.9
    ## 1328       33653         Caradoc         Caradoc     460.9    449.5
    ## 1363       33653       Costonian     Longvillian     460.9    455.8
    ## 1434       33653       Costonian       Harnagian     460.9    455.8
    ## 1440       33653  Late Llandeilo  Late Llandeilo     460.9    449.5
    ## 1467       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 2121       33653       Soudleyan   Marshbrookian     457.5    452.0
    ## 2126       33653       Costonian       Harnagian     460.9    455.8
    ## 2152       33653       Costonian       Harnagian     460.9    455.8
    ## 2175       33653       Costonian       Harnagian     460.9    455.8
    ## 2180       33653       Llandeilo       Llandeilo     466.0    449.5
    ## 2216       33653         Caradoc         Caradoc     460.9    449.5
    ## 2267       33653       Llandeilo       Llandeilo     466.0    449.5
    ## 2290       33653        Llanvirn       Llandeilo     466.0    449.5
    ## 2315       33653          Arenig          Arenig     478.6    466.0
    ## 2334       33653         Caradoc         Caradoc     460.9    449.5
    ## 2359       33653       Llandeilo         Caradoc     466.0    449.5
    ## 2378       33653         Caradoc         Caradoc     460.9    449.5
    ## 2386       33653         Caradoc         Caradoc     460.9    449.5
    ## 2422       33653      Caradocian      Caradocian     460.9    449.5
    ## 2563       33653      Caradocian      Caradocian     460.9    449.5
    ## 2589       33653      Caradocian      Caradocian     460.9    449.5
    ## 2595       33653      Caradocian      Caradocian     460.9    449.5
    ## 2611       33653      Caradocian      Caradocian     460.9    449.5
    ## 3472       33653       Llandeilo       Llandeilo     466.0    449.5
    ## 3478       33653        Llanvirn        Llanvirn     466.0    460.9
    ## 3480       33653       Llandeilo       Llandeilo     466.0    449.5
    ## 3547       33653         Caradoc         Caradoc     460.9    449.5
    ## 3841       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 3918       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4098       33653      Shermanian      Shermanian     460.9    449.5
    ## 4103       33653      Shermanian      Shermanian     460.9    449.5
    ## 4108       33653         Caradoc         Caradoc     460.9    449.5
    ## 4228      306404      Caradocian      Caradocian     460.9    449.5
    ## 4330       33653 Late Ordovician Late Ordovician     458.4    443.4
    ## 4418       33653      Caradocian      Caradocian     460.9    449.5
    ## 4660       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4680       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4681       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4690       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4693       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4699       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4700       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4707       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4708       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4717       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4721       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4722       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4760       33653      Gisbornian      Gisbornian     460.9    456.1
    ## 4769       33653       Eastonian       Eastonian     456.1    449.5
    ## 5875      306404        Sandbian        Sandbian     458.4    453.0
    ## 5877       33653          Katian          Katian     453.0    445.2
    ## 5879       33653          Katian          Katian     453.0    445.2
    ## 5880       33653          Katian          Katian     453.0    445.2
    ##      reference_no   primary_name primary_reso subgenus_name subgenus_reso
    ## 69             13 Dicranograptus         <NA>          <NA>          <NA>
    ## 75             13 Dicranograptus         <NA>          <NA>          <NA>
    ## 78             13 Dicranograptus         <NA>          <NA>          <NA>
    ## 100            13 Dicranograptus         <NA>          <NA>          <NA>
    ## 212            78 Dicranograptus         <NA>          <NA>          <NA>
    ## 228            87 Dicranograptus         <NA>          <NA>          <NA>
    ## 265           103 Dicranograptus         <NA>          <NA>          <NA>
    ## 305           107 Dicranograptus         <NA>          <NA>          <NA>
    ## 314           116 Dicranograptus         <NA>          <NA>          <NA>
    ## 419           227 Dicranograptus         <NA>          <NA>          <NA>
    ## 446           107 Dicranograptus         <NA>          <NA>          <NA>
    ## 491           285 Dicranograptus         <NA>          <NA>          <NA>
    ## 495           285 Dicranograptus         <NA>          <NA>          <NA>
    ## 526           286 Dicranograptus         <NA>          <NA>          <NA>
    ## 555           286 Dicranograptus         <NA>          <NA>          <NA>
    ## 589           287 Dicranograptus         <NA>          <NA>          <NA>
    ## 925           476 Dicranograptus         <NA>          <NA>          <NA>
    ## 931           476 Dicranograptus         <NA>          <NA>          <NA>
    ## 935           476 Dicranograptus         <NA>          <NA>          <NA>
    ## 1014          479 Dicranograptus         <NA>          <NA>          <NA>
    ## 1141          480 Dicranograptus         <NA>          <NA>          <NA>
    ## 1176          480 Dicranograptus         <NA>          <NA>          <NA>
    ## 1254          481 Dicranograptus         <NA>          <NA>          <NA>
    ## 1312          482 Dicranograptus         <NA>          <NA>          <NA>
    ## 1328          613 Dicranograptus         <NA>          <NA>          <NA>
    ## 1363          631 Dicranograptus         <NA>          <NA>          <NA>
    ## 1434          667 Dicranograptus         <NA>          <NA>          <NA>
    ## 1440          632 Dicranograptus         <NA>          <NA>          <NA>
    ## 1467          623 Dicranograptus         <NA>          <NA>          <NA>
    ## 2121          524 Dicranograptus         <NA>          <NA>          <NA>
    ## 2126          524 Dicranograptus         <NA>          <NA>          <NA>
    ## 2152          523 Dicranograptus         <NA>          <NA>          <NA>
    ## 2175          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 2180          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 2216          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 2267          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 2290         3860 Dicranograptus         <NA>          <NA>          <NA>
    ## 2315         3862 Dicranograptus         <NA>          <NA>          <NA>
    ## 2334         3862 Dicranograptus         <NA>          <NA>          <NA>
    ## 2359         3862 Dicranograptus         <NA>          <NA>          <NA>
    ## 2378         3864 Dicranograptus         <NA>          <NA>          <NA>
    ## 2386         3864 Dicranograptus         <NA>          <NA>          <NA>
    ## 2422         6900 Dicranograptus         <NA>          <NA>          <NA>
    ## 2563         7070 Dicranograptus         <NA>          <NA>          <NA>
    ## 2589         7121 Dicranograptus         <NA>          <NA>          <NA>
    ## 2595         7121 Dicranograptus         <NA>          <NA>          <NA>
    ## 2611         7121 Dicranograptus         <NA>          <NA>          <NA>
    ## 3472          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 3478          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 3480          526 Dicranograptus         <NA>          <NA>          <NA>
    ## 3547        15106 Dicranograptus         <NA>          <NA>          <NA>
    ## 3841        18179 Dicranograptus         <NA>          <NA>          <NA>
    ## 3918        18428 Dicranograptus         <NA>          <NA>          <NA>
    ## 4098        25968 Dicranograptus         <NA>          <NA>          <NA>
    ## 4103        25968 Dicranograptus         <NA>          <NA>          <NA>
    ## 4108        26007 Dicranograptus         <NA>          <NA>          <NA>
    ## 4228         6121 Dicranograptus         <NA>          <NA>          <NA>
    ## 4330        36540 Dicranograptus         <NA>          <NA>          <NA>
    ## 4418        37212 Dicranograptus         <NA>          <NA>          <NA>
    ## 4660        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4680        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4681        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4690        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4693        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4699        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4700        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4707        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4708        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4717        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4721        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4722        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4760        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 4769        46966 Dicranograptus         <NA>          <NA>          <NA>
    ## 5875        52829 Dicranograptus         <NA>          <NA>          <NA>
    ## 5877        52829 Dicranograptus         <NA>          <NA>          <NA>
    ## 5879        52829 Dicranograptus         <NA>          <NA>          <NA>
    ## 5880        52829 Dicranograptus         <NA>          <NA>          <NA>
    ##      species_name species_reso subgenus subgenus_no          genus
    ## 69            sp.         <NA>       NA          NA Dicranograptus
    ## 75            sp.         <NA>       NA          NA Dicranograptus
    ## 78            sp.         <NA>       NA          NA Dicranograptus
    ## 100           sp.         <NA>       NA          NA Dicranograptus
    ## 212           sp.         <NA>       NA          NA Dicranograptus
    ## 228           sp.         <NA>       NA          NA Dicranograptus
    ## 265           sp.         <NA>       NA          NA Dicranograptus
    ## 305           sp.         <NA>       NA          NA Dicranograptus
    ## 314           sp.         <NA>       NA          NA Dicranograptus
    ## 419           sp.         <NA>       NA          NA Dicranograptus
    ## 446           sp.         <NA>       NA          NA Dicranograptus
    ## 491           sp.         <NA>       NA          NA Dicranograptus
    ## 495           sp.         <NA>       NA          NA Dicranograptus
    ## 526           sp.         <NA>       NA          NA Dicranograptus
    ## 555           sp.         <NA>       NA          NA Dicranograptus
    ## 589           sp.         <NA>       NA          NA Dicranograptus
    ## 925           sp.         <NA>       NA          NA Dicranograptus
    ## 931           sp.         <NA>       NA          NA Dicranograptus
    ## 935           sp.         <NA>       NA          NA Dicranograptus
    ## 1014          sp.         <NA>       NA          NA Dicranograptus
    ## 1141          sp.         <NA>       NA          NA Dicranograptus
    ## 1176          sp.         <NA>       NA          NA Dicranograptus
    ## 1254          sp.         <NA>       NA          NA Dicranograptus
    ## 1312          sp.         <NA>       NA          NA Dicranograptus
    ## 1328          sp.         <NA>       NA          NA Dicranograptus
    ## 1363          sp.         <NA>       NA          NA Dicranograptus
    ## 1434          sp.         <NA>       NA          NA Dicranograptus
    ## 1440          sp.         <NA>       NA          NA Dicranograptus
    ## 1467          sp.         <NA>       NA          NA Dicranograptus
    ## 2121          sp.         <NA>       NA          NA Dicranograptus
    ## 2126          sp.         <NA>       NA          NA Dicranograptus
    ## 2152          sp.         <NA>       NA          NA Dicranograptus
    ## 2175          sp.         <NA>       NA          NA Dicranograptus
    ## 2180          sp.         <NA>       NA          NA Dicranograptus
    ## 2216          sp.         <NA>       NA          NA Dicranograptus
    ## 2267          sp.         <NA>       NA          NA Dicranograptus
    ## 2290          sp.         <NA>       NA          NA Dicranograptus
    ## 2315          sp.         <NA>       NA          NA Dicranograptus
    ## 2334          sp.         <NA>       NA          NA Dicranograptus
    ## 2359          sp.         <NA>       NA          NA Dicranograptus
    ## 2378          sp.         <NA>       NA          NA Dicranograptus
    ## 2386          sp.         <NA>       NA          NA Dicranograptus
    ## 2422  brevicaulis         <NA>       NA          NA Dicranograptus
    ## 2563          sp.         <NA>       NA          NA Dicranograptus
    ## 2589          sp.         <NA>       NA          NA Dicranograptus
    ## 2595          sp.         <NA>       NA          NA Dicranograptus
    ## 2611          sp.         <NA>       NA          NA Dicranograptus
    ## 3472          sp.         <NA>       NA          NA Dicranograptus
    ## 3478          sp.         <NA>       NA          NA Dicranograptus
    ## 3480          sp.         <NA>       NA          NA Dicranograptus
    ## 3547          sp.         <NA>       NA          NA Dicranograptus
    ## 3841   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 3918   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4098   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4103   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4108     clingani         <NA>       NA          NA Dicranograptus
    ## 4228      ramosus         aff.       NA          NA Dicranograptus
    ## 4330          sp.         <NA>       NA          NA Dicranograptus
    ## 4418    contortus            ?       NA          NA Dicranograptus
    ## 4660  brevicaulis          cf.       NA          NA Dicranograptus
    ## 4680    contortus         <NA>       NA          NA Dicranograptus
    ## 4681     spinifer          cf.       NA          NA Dicranograptus
    ## 4690    contortus         <NA>       NA          NA Dicranograptus
    ## 4693   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4699    contortus         <NA>       NA          NA Dicranograptus
    ## 4700   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4707    contortus         <NA>       NA          NA Dicranograptus
    ## 4708   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4717   nicholsoni         <NA>       NA          NA Dicranograptus
    ## 4721        kirki          cf.       NA          NA Dicranograptus
    ## 4722     spinifer         <NA>       NA          NA Dicranograptus
    ## 4760  brevicaulis          cf.       NA          NA Dicranograptus
    ## 4769        kirki          cf.       NA          NA Dicranograptus
    ## 5875      ramosus         <NA>       NA          NA Dicranograptus
    ## 5877        hians         <NA>       NA          NA Dicranograptus
    ## 5879        hians         <NA>       NA          NA Dicranograptus
    ## 5880        hians         <NA>       NA          NA Dicranograptus
    ##      genus_no           family family_no       order order_no
    ## 69      33653 Dicranograptidae    306398 Bireclinata   306262
    ## 75      33653 Dicranograptidae    306398 Bireclinata   306262
    ## 78      33653 Dicranograptidae    306398 Bireclinata   306262
    ## 100     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 212     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 228     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 265     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 305     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 314     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 419     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 446     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 491     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 495     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 526     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 555     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 589     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 925     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 931     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 935     33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1014    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1141    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1176    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1254    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1312    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1328    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1363    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1434    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1440    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 1467    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2121    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2126    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2152    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2175    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2180    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2216    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2267    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2290    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2315    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2334    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2359    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2378    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2386    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2422    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2563    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2589    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2595    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 2611    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 3472    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 3478    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 3480    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 3547    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 3841    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 3918    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4098    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4103    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4108    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4228    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4330    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4418    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4660    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4680    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4681    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4690    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4693    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4699    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4700    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4707    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4708    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4717    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4721    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4722    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4760    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 4769    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 5875    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 5877    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 5879    33653 Dicranograptidae    306398 Bireclinata   306262
    ## 5880    33653 Dicranograptidae    306398 Bireclinata   306262
    ##              class class_no       phylum phylum_no           authorizer
    ## 69   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 75   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 78   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 100  Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 212  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 228  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 265  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 305  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 314  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 419  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 446  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 491  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 495  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 526  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 555  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 589  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 925  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 931  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 935  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1014 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1141 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1176 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1254 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1312 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1328 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1363 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1434 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1440 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1467 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2121 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2126 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2152 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2175 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2180 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2216 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2267 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2290 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2315 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2334 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2359 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2378 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2386 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2422 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2563 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2589 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2595 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2611 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 3472 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3478 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3480 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3547 Graptolithina    33534 Hemichordata     33518       Patzkowsky, M.
    ## 3841 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3918 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 4098 Graptolithina    33534 Hemichordata     33518            Ivany, L.
    ## 4103 Graptolithina    33534 Hemichordata     33518            Ivany, L.
    ## 4108 Graptolithina    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4228 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 4330 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4418 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4660 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4680 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4681 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4690 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4693 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4699 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4700 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4707 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4708 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4717 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4721 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4722 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4760 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4769 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5875 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 5877 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 5879 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 5880 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ##                   enterer             modifier
    ## 69            Sommers, M.              unknown
    ## 75            Sommers, M.            Alroy, J.
    ## 78            Sommers, M.              unknown
    ## 100           Sommers, M.              unknown
    ## 212  Novack-Gottshall, P.           Wagner, P.
    ## 228  Novack-Gottshall, P.              unknown
    ## 265  Novack-Gottshall, P.              unknown
    ## 305  Novack-Gottshall, P. Novack-Gottshall, P.
    ## 314  Novack-Gottshall, P.              unknown
    ## 419  Novack-Gottshall, P.              unknown
    ## 446  Novack-Gottshall, P.              unknown
    ## 491  Novack-Gottshall, P.              unknown
    ## 495  Novack-Gottshall, P.              unknown
    ## 526  Novack-Gottshall, P.              unknown
    ## 555  Novack-Gottshall, P.              unknown
    ## 589  Novack-Gottshall, P.              unknown
    ## 925  Novack-Gottshall, P.              unknown
    ## 931  Novack-Gottshall, P.              unknown
    ## 935  Novack-Gottshall, P.              unknown
    ## 1014 Novack-Gottshall, P.              unknown
    ## 1141 Novack-Gottshall, P.              unknown
    ## 1176 Novack-Gottshall, P.              unknown
    ## 1254 Novack-Gottshall, P.              unknown
    ## 1312 Novack-Gottshall, P.              unknown
    ## 1328 Novack-Gottshall, P.              unknown
    ## 1363 Novack-Gottshall, P.              unknown
    ## 1434 Novack-Gottshall, P.              unknown
    ## 1440 Novack-Gottshall, P.              unknown
    ## 1467 Novack-Gottshall, P.              unknown
    ## 2121 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2126 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2152 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2175 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2180 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2216 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2267 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2290 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2315 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2334 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2359 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2378 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2386 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2422           Hanson, T.              unknown
    ## 2563           Hanson, T.              unknown
    ## 2589           Hanson, T.              unknown
    ## 2595           Hanson, T.              unknown
    ## 2611           Hanson, T.              unknown
    ## 3472 Novack-Gottshall, P.              unknown
    ## 3478 Novack-Gottshall, P.              unknown
    ## 3480 Novack-Gottshall, P.              unknown
    ## 3547             Krug, Z.              unknown
    ## 3841            Hendy, A.              unknown
    ## 3918            Hendy, A.              unknown
    ## 4098             Wall, P.              unknown
    ## 4103             Wall, P.              unknown
    ## 4108            Hearn, P.              unknown
    ## 4228           Wagner, P.              unknown
    ## 4330            Kolbe, S.              unknown
    ## 4418            Kolbe, S.              unknown
    ## 4660           Krause, M.              unknown
    ## 4680           Krause, M.              unknown
    ## 4681           Krause, M.              unknown
    ## 4690           Krause, M.              unknown
    ## 4693           Krause, M.              unknown
    ## 4699           Krause, M.              unknown
    ## 4700           Krause, M.              unknown
    ## 4707           Krause, M.              unknown
    ## 4708           Krause, M.              unknown
    ## 4717           Krause, M.              unknown
    ## 4721           Krause, M.              unknown
    ## 4722           Krause, M.              unknown
    ## 4760           Krause, M.              unknown
    ## 4769           Krause, M.           Krause, M.
    ## 5875           Wagner, P.           Wagner, P.
    ## 5877           Wagner, P.              unknown
    ## 5879           Wagner, P.           Wagner, P.
    ## 5880           Wagner, P.           Wagner, P.
    ## 
    ## $Diplograptidae
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 32            2763  occurrence      NA       NA           297
    ## 39            2833  occurrence      NA       NA           303
    ## 56            3261  occurrence      NA       NA           321
    ## 58            3357  occurrence      NA       NA           327
    ## 66            3398  occurrence      NA       NA           328
    ## 74            3464  occurrence      NA       NA           331
    ## 77            3789  occurrence      NA       NA           339
    ## 83            3819  occurrence      NA       NA           340
    ## 89            4357  occurrence      NA       NA           366
    ## 94            4635  occurrence      NA       NA           379
    ## 105           4692  occurrence      NA       NA           380
    ## 110           4755  occurrence      NA       NA           383
    ## 115           4838  occurrence      NA       NA           384
    ## 117           4921  occurrence      NA       NA           385
    ## 120           5001  occurrence      NA       NA           386
    ## 122           5128  occurrence      NA       NA           388
    ## 128           5926  occurrence      NA       NA           453
    ## 131           5943  occurrence      NA       NA           454
    ## 152           6942  occurrence      NA       NA           491
    ## 156           7033  occurrence      NA       NA           496
    ## 181           8958  occurrence      NA       NA           403
    ## 192           9060  occurrence      NA       NA           418
    ## 194           9367  occurrence      NA       NA           436
    ## 214          36014  occurrence      NA       NA          2655
    ## 226          38196  occurrence      NA       NA          2709
    ## 233          41894  occurrence      NA       NA          3281
    ## 234          41895  occurrence      NA       NA          3281
    ## 236          41899  occurrence      NA       NA          3282
    ## 237          41900  occurrence      NA       NA          3282
    ## 257          48493  occurrence      NA       NA          2764
    ## 259          48597  occurrence      NA       NA          2767
    ## 261          48680  occurrence      NA       NA          2769
    ## 264          48730  occurrence      NA       NA          2770
    ## 267          48758  occurrence      NA       NA          2771
    ## 269          48768  occurrence      NA       NA          2772
    ## 273          48777  occurrence      NA       NA          2773
    ## 276          48862  occurrence      NA       NA          2931
    ## 283          48926  occurrence      NA       NA          2933
    ## 294          49044  occurrence      NA       NA          2941
    ## 298          49335  occurrence      NA       NA          2949
    ## 303          49365  occurrence      NA       NA          2950
    ## 312          49390  occurrence      NA       NA          3179
    ## 400          51647  occurrence      NA       NA          3857
    ## 411          51940  occurrence      NA       NA          3863
    ## 415          51979  occurrence      NA       NA          3863
    ## 416          52041  occurrence      NA       NA          3865
    ## 418          52102  occurrence      NA       NA          3865
    ## 422          52218  occurrence      NA       NA          3874
    ## 436          93748  occurrence      NA       NA          6986
    ## 444         105282  occurrence      NA       NA          2951
    ## 472         105401  occurrence      NA       NA          4665
    ## 482         105411  occurrence      NA       NA          4666
    ## 489         105418  occurrence      NA       NA          4667
    ## 493         105422  occurrence      NA       NA          4668
    ## 502         105431  occurrence      NA       NA          4669
    ## 511         105459  occurrence      NA       NA          4674
    ## 523         105472  occurrence      NA       NA          4676
    ## 529         105478  occurrence      NA       NA          4677
    ## 534         105483  occurrence      NA       NA          4678
    ## 544         105511  occurrence      NA       NA          4682
    ## 549         105516  occurrence      NA       NA          4683
    ## 553         105539  occurrence      NA       NA          4685
    ## 560         105552  occurrence      NA       NA          4686
    ## 571         105599  occurrence      NA       NA          4688
    ## 579         105705  occurrence      NA       NA          4708
    ## 586         105763  occurrence      NA       NA          4710
    ## 587         105789  occurrence      NA       NA          4711
    ## 627         106410  occurrence      NA       NA          4747
    ## 634         106417  occurrence      NA       NA          4748
    ## 641         106424  occurrence      NA       NA          4749
    ## 659         106623  occurrence      NA       NA          5134
    ## 665         106629  occurrence      NA       NA          5135
    ## 666         106630  occurrence      NA       NA          5135
    ## 670         106635  occurrence      NA       NA          5136
    ## 698         106795  occurrence      NA       NA          5337
    ## 706         106832  occurrence      NA       NA          5405
    ## 725         106935  occurrence      NA       NA          5427
    ## 729         106978  occurrence      NA       NA          7252
    ## 734         106983  occurrence      NA       NA          7253
    ## 738         107009  occurrence      NA       NA          7258
    ## 741         107012  occurrence      NA       NA          7259
    ## 746         107017  occurrence      NA       NA          7261
    ## 759         107081  occurrence      NA       NA          7289
    ## 791         107235  occurrence      NA       NA          7380
    ## 795         107239  occurrence      NA       NA          7381
    ## 808         107302  occurrence      NA       NA          7636
    ## 813         107308  occurrence      NA       NA          7637
    ## 819         107325  occurrence      NA       NA          7641
    ## 837         107398  occurrence      NA       NA          7654
    ## 865         107520  occurrence      NA       NA          7677
    ## 887         107641  occurrence      NA       NA          7696
    ## 891         107650  occurrence      NA       NA          7699
    ## 918         107712  occurrence      NA       NA          7705
    ## 920         107714  occurrence      NA       NA          7706
    ## 923         107717  occurrence      NA       NA          7707
    ## 929         107723  occurrence      NA       NA          7709
    ## 933         107727  occurrence      NA       NA          7710
    ## 949         107746  occurrence      NA       NA          7713
    ## 960         107837  occurrence      NA       NA          7721
    ## 968         107864  occurrence      NA       NA          7725
    ## 1000        108037  occurrence      NA       NA          7747
    ## 1003        108045  occurrence      NA       NA          7748
    ## 1012        108069  occurrence      NA       NA          7751
    ## 1016        108073  occurrence      NA       NA          7752
    ## 1027        108085  occurrence      NA       NA          7754
    ## 1059        108140  occurrence      NA       NA          7761
    ## 1086        108181  occurrence      NA       NA          7767
    ## 1090        108246  occurrence      NA       NA          7770
    ## 1101        108258  occurrence      NA       NA          7771
    ## 1130        108303  occurrence      NA       NA          7775
    ## 1138        108384  occurrence      NA       NA          7782
    ## 1163        108411  occurrence      NA       NA          7792
    ## 1166        108415  occurrence      NA       NA          7793
    ## 1213        108488  occurrence      NA       NA          7808
    ## 1215        108514  occurrence      NA       NA          7811
    ## 1221        108521  occurrence      NA       NA          7812
    ## 1229        108529  occurrence      NA       NA          7813
    ## 1247        108579  occurrence      NA       NA          7833
    ## 1252        108588  occurrence      NA       NA          7834
    ## 1273        108747  occurrence      NA       NA          7847
    ## 1285        108828  occurrence      NA       NA          7871
    ## 1290        108877  occurrence      NA       NA          7881
    ## 1305        109256  occurrence      NA       NA          7944
    ## 1309        109262  occurrence      NA       NA          7945
    ## 1315        110641  occurrence      NA       NA          8370
    ## 1316        110686  occurrence      NA       NA          8373
    ## 1317        110687  occurrence      NA       NA          8373
    ## 1360        118497  occurrence      NA       NA          8858
    ## 1394        118645  occurrence      NA       NA          8874
    ## 1412        118725  occurrence      NA       NA          8886
    ## 1416        118729  occurrence      NA       NA          8887
    ## 1432        118757  occurrence      NA       NA          8889
    ## 1465        118971  occurrence      NA       NA          9035
    ## 1473        118979  occurrence      NA       NA          9036
    ## 1554        144292  occurrence      NA       NA         12582
    ## 1556        144304  occurrence      NA       NA         12583
    ## 1566        148830  occurrence      NA       NA         13132
    ## 1568        148832  occurrence      NA       NA         13132
    ## 1569        149796  occurrence      NA       NA         13261
    ## 1571        149798  occurrence      NA       NA         13261
    ## 1573        151455  occurrence      NA       NA         13492
    ## 1574        151456  occurrence      NA       NA         13492
    ## 1575        151457  occurrence      NA       NA         13492
    ## 1579        151461  occurrence      NA       NA         13493
    ## 1580        151462  occurrence      NA       NA         13493
    ## 1581        151463  occurrence      NA       NA         13493
    ## 1582        151464  occurrence      NA       NA         13493
    ## 1586        151468  occurrence      NA       NA         13493
    ## 1590        154397  occurrence      NA       NA         13704
    ## 1591        154398  occurrence      NA       NA         13704
    ## 1596        154403  occurrence      NA       NA         13705
    ## 1597        154404  occurrence      NA       NA         13705
    ## 1599        154406  occurrence      NA       NA         13706
    ## 1600        154407  occurrence      NA       NA         13706
    ## 1601        154408  occurrence      NA       NA         13706
    ## 1605        154412  occurrence      NA       NA         13707
    ## 1606        154413  occurrence      NA       NA         13707
    ## 1612        154419  occurrence      NA       NA         13708
    ## 1613        154420  occurrence      NA       NA         13708
    ## 1637        154444  occurrence      NA       NA         13709
    ## 1648        154455  occurrence      NA       NA         13710
    ## 1839        157888  occurrence      NA       NA         13988
    ## 2120        240570  occurrence      NA       NA          8527
    ## 2124        240574  occurrence      NA       NA          8528
    ## 2128        240578  occurrence      NA       NA          8529
    ## 2140        240642  occurrence      NA       NA          8534
    ## 2150        240654  occurrence      NA       NA          8535
    ## 2166        240812  occurrence      NA       NA          8549
    ## 2173        240846  occurrence      NA       NA          8552
    ## 2185        240881  occurrence      NA       NA          8557
    ## 2192        240896  occurrence      NA       NA          8558
    ## 2199        240918  occurrence      NA       NA          8561
    ## 2202        240951  occurrence      NA       NA          8563
    ## 2211        240965  occurrence      NA       NA          8564
    ## 2214        240980  occurrence      NA       NA          8565
    ## 2224        241007  occurrence      NA       NA          8567
    ## 2234        241044  occurrence      NA       NA          8569
    ## 2239        241063  occurrence      NA       NA          8571
    ## 2246        241070  occurrence      NA       NA          8572
    ## 2256        241092  occurrence      NA       NA          8575
    ## 2291        242118  occurrence      NA       NA         20764
    ## 2317        242356  occurrence      NA       NA         20792
    ## 2325        242371  occurrence      NA       NA         20797
    ## 2328        242376  occurrence      NA       NA         20796
    ## 2341        242429  occurrence      NA       NA         20803
    ## 2347        242439  occurrence      NA       NA         20805
    ## 2362        242491  occurrence      NA       NA         20808
    ## 2368        242515  occurrence      NA       NA         23581
    ## 2376        242531  occurrence      NA       NA         23591
    ## 2379        242535  occurrence      NA       NA         23592
    ## 2399        246238  occurrence      NA       NA         24117
    ## 2400        246239  occurrence      NA       NA         24117
    ## 2413        251704  occurrence      NA       NA         24518
    ## 2424        253008  occurrence      NA       NA         24603
    ## 2425        253009  occurrence      NA       NA         24603
    ## 2437        254226  occurrence      NA       NA         24615
    ## 2456        255102  occurrence      NA       NA         24761
    ## 2459        255136  occurrence      NA       NA         24581
    ## 2463        255140  occurrence      NA       NA         24769
    ## 2464        255141  occurrence      NA       NA         24769
    ## 2466        255143  occurrence      NA       NA         24770
    ## 2501        259589  occurrence      NA       NA         25093
    ## 2502        259590  occurrence      NA       NA         25093
    ## 2505        259638  occurrence      NA       NA         25098
    ## 2507        259653  occurrence      NA       NA         25101
    ## 2508        259654  occurrence      NA       NA         25101
    ## 2518        259738  occurrence      NA       NA         25113
    ## 2520        259761  occurrence      NA       NA         25116
    ## 2521        259778  occurrence      NA       NA         25117
    ## 2525        260369  occurrence      NA       NA         25167
    ## 2526        260370  occurrence      NA       NA         25167
    ## 2527        260371  occurrence      NA       NA         25167
    ## 2528        260372  occurrence      NA       NA         25167
    ## 2530        260374  occurrence      NA       NA         25168
    ## 2562        262273  occurrence      NA       NA         25338
    ## 2565        262297  occurrence      NA       NA         25343
    ## 2585        263697  occurrence      NA       NA         25512
    ## 2587        263699  occurrence      NA       NA         25513
    ## 2593        263714  occurrence      NA       NA         25516
    ## 2644        264350  occurrence      NA       NA         20846
    ## 2646        264537  occurrence      NA       NA         20876
    ## 2661        264945  occurrence      NA       NA         20931
    ## 2706        265970  occurrence      NA       NA         25566
    ## 2707        265981  occurrence      NA       NA         25568
    ## 2708        266001  occurrence      NA       NA         25570
    ## 2710        266023  occurrence      NA       NA         25570
    ## 2755        272276  occurrence      NA       NA         26089
    ## 2793        275168  occurrence      NA       NA         26273
    ## 2797        275717  occurrence      NA       NA         26295
    ## 2798        275718  occurrence      NA       NA         26295
    ## 2799        275719  occurrence      NA       NA         26295
    ## 2804        275770  occurrence      NA       NA         26296
    ## 2806        275785  occurrence      NA       NA         26297
    ## 2807        275798  occurrence      NA       NA         26299
    ## 2809        275810  occurrence      NA       NA         26302
    ## 2810        275811  occurrence      NA       NA         26302
    ## 2884        285928  occurrence      NA       NA         27197
    ## 2891        285951  occurrence      NA       NA         27203
    ## 2892        285952  occurrence      NA       NA         27203
    ## 2893        285953  occurrence      NA       NA         27203
    ## 2934        286767  occurrence      NA       NA         27337
    ## 2935        286768  occurrence      NA       NA         27337
    ## 2943        287036  occurrence      NA       NA         27362
    ## 2948        287240  occurrence      NA       NA         27388
    ## 3021        287552  occurrence      NA       NA         27454
    ## 3108        290629  occurrence      NA       NA         27739
    ## 3110        290632  occurrence      NA       NA         27739
    ## 3116        290640  occurrence      NA       NA         27741
    ## 3127        290862  occurrence      NA       NA         27765
    ## 3128        290863  occurrence      NA       NA         27765
    ## 3129        290864  occurrence      NA       NA         27765
    ## 3148        291068  occurrence      NA       NA         27776
    ## 3149        291069  occurrence      NA       NA         27776
    ## 3173        291182  occurrence      NA       NA         27782
    ## 3182        291191  occurrence      NA       NA         27782
    ## 3199        291403  occurrence      NA       NA         27797
    ## 3200        291404  occurrence      NA       NA         27797
    ## 3202        291409  occurrence      NA       NA         27798
    ## 3246        292390  occurrence      NA       NA         27838
    ## 3248        292392  occurrence      NA       NA         27838
    ## 3276        292476  occurrence      NA       NA         27849
    ## 3290        292677  occurrence      NA       NA         27859
    ## 3318        292715  occurrence      NA       NA         27868
    ## 3353        292926  occurrence      NA       NA         27898
    ## 3358        292946  occurrence      NA       NA         27902
    ## 3366        292983  occurrence      NA       NA         27904
    ## 3377        293066  occurrence      NA       NA         27910
    ## 3386        293086  occurrence      NA       NA         27911
    ## 3403        368957  occurrence      NA       NA         34895
    ## 3462        445028  occurrence      NA       NA         43771
    ## 3473        446193  occurrence      NA       NA          8680
    ## 3479        446216  occurrence      NA       NA          8681
    ## 3485        446263  occurrence      NA       NA          8686
    ## 3530        472366  occurrence      NA       NA         46939
    ## 3541        538630  occurrence      NA       NA         56000
    ## 3545        538657  occurrence      NA       NA         56002
    ## 3677        596952  occurrence      NA       NA         63276
    ## 3842        598665  occurrence      NA       NA         63445
    ## 3847        598673  occurrence      NA       NA         63446
    ## 3848        598674  occurrence      NA       NA         63447
    ## 3849        598675  occurrence      NA       NA         63448
    ## 3857        598683  occurrence      NA       NA         63444
    ## 3859        601755  occurrence      NA       NA         63972
    ## 3866        601763  occurrence      NA       NA         63971
    ## 3867        601764  occurrence      NA       NA         63971
    ## 3894        601794  occurrence      NA       NA         63968
    ## 3903        601806  occurrence      NA       NA         63967
    ## 3912        601817  occurrence      NA       NA         63966
    ## 3919        601836  occurrence      NA       NA         63956
    ## 3937        601857  occurrence      NA       NA         63957
    ## 3941        601861  occurrence      NA       NA         63957
    ## 3942        601862  occurrence      NA       NA         63957
    ## 3949        601872  occurrence      NA       NA         63958
    ## 3956        601881  occurrence      NA       NA         63960
    ## 3968        601893  occurrence      NA       NA         63961
    ## 3979        601907  occurrence      NA       NA         63962
    ## 3983        601911  occurrence      NA       NA         63963
    ## 3998        601927  occurrence      NA       NA         63964
    ## 4011        601941  occurrence      NA       NA         63965
    ## 4023        605528  occurrence      NA       NA         64543
    ## 4038        679894  occurrence      NA       NA         73357
    ## 4041        703604  occurrence      NA       NA         75542
    ## 4046        703613  occurrence      NA       NA         75544
    ## 4051        703626  occurrence      NA       NA         75546
    ## 4061        710497  occurrence      NA       NA         76077
    ## 4062        710498  occurrence      NA       NA         76077
    ## 4067        710535  occurrence      NA       NA         76079
    ## 4072        712205  occurrence      NA       NA         76336
    ## 4075        712218  occurrence      NA       NA         76337
    ## 4096        715588  occurrence      NA       NA         76744
    ## 4097        715620  occurrence      NA       NA         76746
    ## 4099        715626  occurrence      NA       NA         76748
    ## 4101        715631  occurrence      NA       NA         76750
    ## 4102        715639  occurrence      NA       NA         76751
    ## 4104        716398  occurrence      NA       NA         76902
    ## 4110        716414  occurrence      NA       NA         76905
    ## 4113        716451  occurrence      NA       NA         76909
    ## 4115        716482  occurrence      NA       NA         76912
    ## 4138        718087  occurrence      NA       NA         77083
    ## 4141        718183  occurrence      NA       NA         77102
    ## 4142        718184  occurrence      NA       NA         77102
    ## 4150        719310  occurrence      NA       NA         77187
    ## 4166        748935  occurrence      NA       NA         80104
    ## 4167        748936  occurrence      NA       NA         80104
    ## 4256        916252  occurrence      NA       NA        104858
    ## 4257        916253  occurrence      NA       NA        104858
    ## 4266        916263  occurrence      NA       NA        104860
    ## 4267        916264  occurrence      NA       NA        104860
    ## 4286        916414  occurrence      NA       NA        104868
    ## 4292        917387  occurrence      NA       NA        104491
    ## 4293        917395  occurrence      NA       NA        104492
    ## 4302        954505  occurrence      NA       NA        111637
    ## 4303        954524  occurrence      NA       NA        111639
    ## 4305        954531  occurrence      NA       NA        111643
    ## 4309        955077  occurrence      NA       NA        111705
    ## 4316        955084  occurrence      NA       NA        111708
    ## 4317        955085  occurrence      NA       NA        111709
    ## 4320        955088  occurrence      NA       NA        111711
    ## 4325        955095  occurrence      NA       NA        111713
    ## 4332        955103  occurrence      NA       NA        111718
    ## 4333        955104  occurrence      NA       NA        111719
    ## 4340        955113  occurrence      NA       NA        111726
    ## 4345        969075  occurrence      NA       NA        114843
    ## 4350        969080  occurrence      NA       NA        114844
    ## 4353        969084  occurrence      NA       NA        114845
    ## 4354        969085  occurrence      NA       NA        114845
    ## 4355        969086  occurrence      NA       NA        114845
    ## 4358        969089  occurrence      NA       NA        114846
    ## 4366        969118  occurrence      NA       NA        114847
    ## 4379        969136  occurrence      NA       NA        114848
    ## 4386        969146  occurrence      NA       NA        114849
    ## 4391        969151  occurrence      NA       NA        114850
    ## 4402        969163  occurrence      NA       NA        114851
    ## 4413        969184  occurrence      NA       NA        114852
    ## 4414        969185  occurrence      NA       NA        114852
    ## 4436        969210  occurrence      NA       NA        114856
    ## 4444        969230  occurrence      NA       NA        114859
    ## 4498        969904  occurrence      NA       NA        114976
    ## 4501        969916  occurrence      NA       NA        114980
    ## 4516        996584  occurrence      NA       NA        120528
    ## 4522        997019  occurrence      NA       NA        120626
    ## 4662       1139686  occurrence      NA       NA        145227
    ## 4667       1139691  occurrence      NA       NA        145228
    ## 4671       1139695  occurrence      NA       NA        145229
    ## 4673       1139698  occurrence      NA       NA        145230
    ## 4685       1139721  occurrence      NA       NA        145233
    ## 4686       1139722  occurrence      NA       NA        145233
    ## 4695       1139731  occurrence      NA       NA        145236
    ## 4703       1139741  occurrence      NA       NA        145237
    ## 4713       1139751  occurrence      NA       NA        145238
    ## 4725       1139763  occurrence      NA       NA        145240
    ## 4726       1139764  occurrence      NA       NA        145240
    ## 4748       1140637  occurrence      NA       NA        145328
    ## 4756       1140645  occurrence      NA       NA        145330
    ## 4765       1140654  occurrence      NA       NA        145331
    ## 4773       1141828  occurrence      NA       NA        145463
    ## 4774       1141829  occurrence      NA       NA        145464
    ## 4775       1141830  occurrence      NA       NA        145463
    ## 4776       1141832  occurrence      NA       NA        145465
    ## 4777       1141833  occurrence      NA       NA        145469
    ## 4780       1141836  occurrence      NA       NA        145465
    ## 4781       1141837  occurrence      NA       NA        145466
    ## 4782       1141838  occurrence      NA       NA        145467
    ## 4816       1141874  occurrence      NA       NA        145472
    ## 4817       1141875  occurrence      NA       NA        145473
    ## 4818       1141876  occurrence      NA       NA        145474
    ## 4819       1141877  occurrence      NA       NA        145475
    ## 4820       1141878  occurrence      NA       NA        145472
    ## 4821       1141879  occurrence      NA       NA        145473
    ## 4822       1141880  occurrence      NA       NA        145474
    ## 4823       1141881  occurrence      NA       NA        145481
    ## 4824       1141882  occurrence      NA       NA        145473
    ## 4825       1141883  occurrence      NA       NA        145474
    ## 4826       1141884  occurrence      NA       NA        145475
    ## 4827       1141885  occurrence      NA       NA        145476
    ## 4828       1141886  occurrence      NA       NA        145478
    ## 4829       1141887  occurrence      NA       NA        145479
    ## 4830       1141888  occurrence      NA       NA        145480
    ## 4831       1141889  occurrence      NA       NA        145481
    ## 4833       1141891  occurrence      NA       NA        145472
    ## 4834       1141892  occurrence      NA       NA        145473
    ## 4835       1141893  occurrence      NA       NA        145475
    ## 4836       1141894  occurrence      NA       NA        145476
    ## 4837       1141895  occurrence      NA       NA        145477
    ## 4838       1141896  occurrence      NA       NA        145478
    ## 4839       1141897  occurrence      NA       NA        145479
    ## 4883       1141944  occurrence      NA       NA        145489
    ## 4884       1141945  occurrence      NA       NA        145490
    ## 4885       1141946  occurrence      NA       NA        145493
    ## 4886       1141947  occurrence      NA       NA        145494
    ## 4887       1141948  occurrence      NA       NA        145496
    ## 4888       1141949  occurrence      NA       NA        145498
    ## 4889       1141950  occurrence      NA       NA        145489
    ## 4890       1141951  occurrence      NA       NA        145493
    ## 4891       1141952  occurrence      NA       NA        145494
    ## 4892       1141953  occurrence      NA       NA        145495
    ## 4893       1141954  occurrence      NA       NA        145496
    ## 4899       1141960  occurrence      NA       NA        145485
    ## 4900       1141961  occurrence      NA       NA        145486
    ## 4901       1141962  occurrence      NA       NA        145487
    ## 4902       1141963  occurrence      NA       NA        145488
    ## 4903       1141964  occurrence      NA       NA        145495
    ## 4904       1141965  occurrence      NA       NA        145496
    ## 4905       1141966  occurrence      NA       NA        145498
    ## 4906       1141967  occurrence      NA       NA        145484
    ## 4907       1141968  occurrence      NA       NA        145485
    ## 4908       1141969  occurrence      NA       NA        145486
    ## 4909       1141970  occurrence      NA       NA        145487
    ## 4910       1141971  occurrence      NA       NA        145488
    ## 4911       1141972  occurrence      NA       NA        145484
    ## 4912       1141973  occurrence      NA       NA        145485
    ## 4913       1141974  occurrence      NA       NA        145486
    ## 4914       1141975  occurrence      NA       NA        145487
    ## 4915       1141976  occurrence      NA       NA        145488
    ## 4916       1141977  occurrence      NA       NA        145497
    ## 4917       1141978  occurrence      NA       NA        145490
    ## 4918       1141979  occurrence      NA       NA        145491
    ## 4919       1141980  occurrence      NA       NA        145492
    ## 4920       1141981  occurrence      NA       NA        145493
    ## 4921       1141982  occurrence      NA       NA        145494
    ## 4923       1141984  occurrence      NA       NA        145496
    ## 4924       1141985  occurrence      NA       NA        145498
    ## 4925       1141986  occurrence      NA       NA        145496
    ## 4926       1141987  occurrence      NA       NA        145485
    ## 4927       1141988  occurrence      NA       NA        145489
    ## 4928       1141989  occurrence      NA       NA        145490
    ## 4929       1141990  occurrence      NA       NA        145495
    ## 4962       1142798  occurrence      NA       NA        145513
    ## 4963       1142799  occurrence      NA       NA        145514
    ## 4964       1142800  occurrence      NA       NA        145513
    ## 5102       1143750  occurrence      NA       NA        145584
    ## 5103       1143751  occurrence      NA       NA        145584
    ## 5106       1143754  occurrence      NA       NA        145585
    ## 5110       1143758  occurrence      NA       NA        145586
    ## 5114       1143762  occurrence      NA       NA        145587
    ## 5115       1143763  occurrence      NA       NA        145587
    ## 5126       1143784  occurrence      NA       NA        145590
    ## 5127       1143785  occurrence      NA       NA        145590
    ## 5128       1143786  occurrence      NA       NA        145590
    ## 5129       1143787  occurrence      NA       NA        145590
    ## 5130       1143788  occurrence      NA       NA        145590
    ## 5131       1143789  occurrence      NA       NA        145590
    ## 5132       1143790  occurrence      NA       NA        145590
    ## 5150       1143808  occurrence      NA       NA        145591
    ## 5151       1143809  occurrence      NA       NA        145591
    ## 5152       1143810  occurrence      NA       NA        145591
    ## 5153       1143811  occurrence      NA       NA        145591
    ## 5154       1143812  occurrence      NA       NA        145591
    ## 5155       1143813  occurrence      NA       NA        145591
    ## 5167       1143825  occurrence      NA       NA        145592
    ## 5176       1143836  occurrence      NA       NA        145595
    ## 5177       1143837  occurrence      NA       NA        145595
    ## 5195       1143855  occurrence      NA       NA        145596
    ## 5204       1143865  occurrence      NA       NA        145598
    ## 5205       1143866  occurrence      NA       NA        145598
    ## 5248       1143913  occurrence      NA       NA        145606
    ## 5249       1143914  occurrence      NA       NA        145606
    ## 5250       1143915  occurrence      NA       NA        145606
    ## 5251       1143916  occurrence      NA       NA        145606
    ## 5253       1143918  occurrence      NA       NA        145606
    ## 5256       1143921  occurrence      NA       NA        145606
    ## 5260       1143925  occurrence      NA       NA        145606
    ## 5261       1143926  occurrence      NA       NA        145607
    ## 5262       1143927  occurrence      NA       NA        145607
    ## 5263       1143928  occurrence      NA       NA        145607
    ## 5265       1143930  occurrence      NA       NA        145607
    ## 5268       1143933  occurrence      NA       NA        145607
    ## 5270       1143935  occurrence      NA       NA        145607
    ## 5275       1143940  occurrence      NA       NA        145608
    ## 5277       1143942  occurrence      NA       NA        145608
    ## 5281       1143946  occurrence      NA       NA        145608
    ## 5286       1143951  occurrence      NA       NA        145609
    ## 5287       1143952  occurrence      NA       NA        145609
    ## 5289       1143954  occurrence      NA       NA        145609
    ## 5293       1143958  occurrence      NA       NA        145609
    ## 5298       1143963  occurrence      NA       NA        145610
    ## 5299       1143964  occurrence      NA       NA        145612
    ## 5300       1143965  occurrence      NA       NA        145610
    ## 5301       1143966  occurrence      NA       NA        145611
    ## 5302       1143967  occurrence      NA       NA        145612
    ## 5305       1143970  occurrence      NA       NA        145610
    ## 5306       1143971  occurrence      NA       NA        145611
    ## 5307       1143972  occurrence      NA       NA        145612
    ## 5314       1143979  occurrence      NA       NA        145611
    ## 5315       1143980  occurrence      NA       NA        145612
    ## 5319       1143984  occurrence      NA       NA        145611
    ## 5320       1143985  occurrence      NA       NA        145612
    ## 5322       1143987  occurrence      NA       NA        145611
    ## 5323       1143988  occurrence      NA       NA        145612
    ## 5326       1143991  occurrence      NA       NA        145610
    ## 5327       1143992  occurrence      NA       NA        145611
    ## 5330       1144012  occurrence      NA       NA        145615
    ## 5333       1144015  occurrence      NA       NA        145615
    ## 5342       1144114  occurrence      NA       NA        145652
    ## 5343       1144115  occurrence      NA       NA        145653
    ## 5344       1144116  occurrence      NA       NA        145653
    ## 5345       1144117  occurrence      NA       NA        145653
    ## 5346       1144118  occurrence      NA       NA        145653
    ## 5347       1144119  occurrence      NA       NA        145653
    ## 5353       1144126  occurrence      NA       NA        145654
    ## 5354       1144127  occurrence      NA       NA        145654
    ## 5355       1144128  occurrence      NA       NA        145654
    ## 5363       1144140  occurrence      NA       NA        145655
    ## 5364       1144141  occurrence      NA       NA        145655
    ## 5365       1144142  occurrence      NA       NA        145655
    ## 5385       1144162  occurrence      NA       NA        145656
    ## 5486       1144779  occurrence      NA       NA        145613
    ## 5487       1144780  occurrence      NA       NA        145613
    ## 5488       1144781  occurrence      NA       NA        145613
    ## 5490       1144783  occurrence      NA       NA        145613
    ## 5495       1144788  occurrence      NA       NA        145613
    ## 5496       1144789  occurrence      NA       NA        145613
    ## 5506       1144799  occurrence      NA       NA        145737
    ## 5508       1144801  occurrence      NA       NA        145737
    ## 5513       1144806  occurrence      NA       NA        145737
    ## 5515       1144808  occurrence      NA       NA        145737
    ## 5518       1144811  occurrence      NA       NA        145737
    ## 5523       1144816  occurrence      NA       NA        145737
    ## 5524       1144817  occurrence      NA       NA        145739
    ## 5525       1144818  occurrence      NA       NA        145739
    ## 5530       1144823  occurrence      NA       NA        145739
    ## 5532       1144825  occurrence      NA       NA        145739
    ## 5538       1144831  occurrence      NA       NA        145739
    ## 5544       1144837  occurrence      NA       NA        145739
    ## 5547       1144840  occurrence      NA       NA        145739
    ## 5548       1144841  occurrence      NA       NA        145740
    ## 5549       1144842  occurrence      NA       NA        145740
    ## 5554       1144847  occurrence      NA       NA        145740
    ## 5559       1144852  occurrence      NA       NA        145740
    ## 5563       1144856  occurrence      NA       NA        145740
    ## 5565       1144858  occurrence      NA       NA        145740
    ## 5567       1144860  occurrence      NA       NA        145741
    ## 5568       1144862  occurrence      NA       NA        145741
    ## 5573       1144867  occurrence      NA       NA        145741
    ## 5575       1144869  occurrence      NA       NA        145741
    ## 5585       1144879  occurrence      NA       NA        145741
    ## 5586       1144880  occurrence      NA       NA        145742
    ## 5587       1144881  occurrence      NA       NA        145742
    ## 5588       1144882  occurrence      NA       NA        145742
    ## 5593       1144887  occurrence      NA       NA        145742
    ## 5598       1144892  occurrence      NA       NA        145743
    ## 5599       1144893  occurrence      NA       NA        145743
    ## 5602       1144896  occurrence      NA       NA        145743
    ## 5606       1144900  occurrence      NA       NA        145744
    ## 5607       1144901  occurrence      NA       NA        145744
    ## 5610       1144904  occurrence      NA       NA        145744
    ## 5611       1144905  occurrence      NA       NA        145744
    ## 5613       1144907  occurrence      NA       NA        145744
    ## 5616       1144910  occurrence      NA       NA        145745
    ## 5617       1144911  occurrence      NA       NA        145745
    ## 5621       1144915  occurrence      NA       NA        145745
    ## 5625       1144919  occurrence      NA       NA        145745
    ## 5631       1144925  occurrence      NA       NA        145746
    ## 5632       1144926  occurrence      NA       NA        145746
    ## 5633       1144927  occurrence      NA       NA        145746
    ## 5637       1144932  occurrence      NA       NA        145746
    ## 5641       1144936  occurrence      NA       NA        145746
    ## 5646       1144941  occurrence      NA       NA        145746
    ## 5670       1144965  occurrence      NA       NA        145750
    ## 5673       1144968  occurrence      NA       NA        145750
    ## 5719       1145091  occurrence      NA       NA        145800
    ## 5724       1145096  occurrence      NA       NA        145800
    ## 5726       1145098  occurrence      NA       NA        145800
    ## 5727       1145099  occurrence      NA       NA        145801
    ## 5731       1145103  occurrence      NA       NA        145801
    ## 5732       1145104  occurrence      NA       NA        145801
    ## 5735       1145107  occurrence      NA       NA        145802
    ## 5740       1145112  occurrence      NA       NA        145802
    ## 5742       1145114  occurrence      NA       NA        145802
    ## 5743       1145115  occurrence      NA       NA        145802
    ## 5745       1145117  occurrence      NA       NA        145802
    ## 5747       1145119  occurrence      NA       NA        145802
    ## 5748       1145120  occurrence      NA       NA        145803
    ## 5752       1145124  occurrence      NA       NA        145803
    ## 5754       1145126  occurrence      NA       NA        145803
    ## 5760       1145132  occurrence      NA       NA        145804
    ## 5764       1145136  occurrence      NA       NA        145804
    ## 5766       1145138  occurrence      NA       NA        145804
    ## 5776       1145148  occurrence      NA       NA        145805
    ## 5783       1145155  occurrence      NA       NA        145805
    ## 5843       1187260  occurrence      NA       NA        153325
    ## 5845       1187297  occurrence      NA       NA        153329
    ## 5871       1218886  occurrence      NA       NA        159343
    ## 5886       1256549  occurrence      NA       NA        166743
    ## 5892       1256954  occurrence      NA       NA        166800
    ## 5896       1257991  occurrence      NA       NA        166909
    ##                          identified_name identified_rank identified_no
    ## 32                    Climacograptus sp.           genus         33636
    ## 39                    Climacograptus sp.           genus         33636
    ## 56                    Climacograptus sp.           genus         33636
    ## 58                    Climacograptus sp.           genus         33636
    ## 66                    Climacograptus sp.           genus         33636
    ## 74                    Climacograptus sp.           genus         33636
    ## 77                    Climacograptus sp.           genus         33636
    ## 83                    Climacograptus sp.           genus         33636
    ## 89                    Climacograptus sp.           genus         33636
    ## 94                    Climacograptus sp.           genus         33636
    ## 105                   Climacograptus sp.           genus         33636
    ## 110                   Climacograptus sp.           genus         33636
    ## 115                   Climacograptus sp.           genus         33636
    ## 117                   Climacograptus sp.           genus         33636
    ## 120                   Climacograptus sp.           genus         33636
    ## 122                   Climacograptus sp.           genus         33636
    ## 128                   Climacograptus sp.           genus         33636
    ## 131                   Climacograptus sp.           genus         33636
    ## 152                   Climacograptus sp.           genus         33636
    ## 156                   Climacograptus sp.           genus         33636
    ## 181                   Climacograptus sp.           genus         33636
    ## 192                   Climacograptus sp.           genus         33636
    ## 194                   Climacograptus sp.           genus         33636
    ## 214                   Climacograptus sp.           genus         33636
    ## 226                   Climacograptus sp.           genus         33636
    ## 233              Climacograptus scalaris         species        316364
    ## 234             Climacograptus innotatus         species         33636
    ## 236              Climacograptus scalaris         species        316364
    ## 237             Climacograptus innotatus         species         33636
    ## 257                   Climacograptus sp.           genus         33636
    ## 259                   Climacograptus sp.           genus         33636
    ## 261                   Climacograptus sp.           genus         33636
    ## 264                   Climacograptus sp.           genus         33636
    ## 267                   Climacograptus sp.           genus         33636
    ## 269                   Climacograptus sp.           genus         33636
    ## 273                   Climacograptus sp.           genus         33636
    ## 276                   Climacograptus sp.           genus         33636
    ## 283                   Climacograptus sp.           genus         33636
    ## 294                   Climacograptus sp.           genus         33636
    ## 298                   Climacograptus sp.           genus         33636
    ## 303                   Climacograptus sp.           genus         33636
    ## 312                   Climacograptus sp.           genus         33636
    ## 400                   Climacograptus sp.           genus         33636
    ## 411                   Climacograptus sp.           genus         33636
    ## 415                     Rectograptus sp.           genus        270339
    ## 416                   Climacograptus sp.           genus         33636
    ## 418                     Rectograptus sp.           genus        270339
    ## 422                     Rectograptus sp.           genus        270339
    ## 436          Climacograptus scharenbergi         species         33636
    ## 444                   Climacograptus sp.           genus         33636
    ## 472                   Climacograptus sp.           genus         33636
    ## 482                   Climacograptus sp.           genus         33636
    ## 489                   Climacograptus sp.           genus         33636
    ## 493                   Climacograptus sp.           genus         33636
    ## 502                   Climacograptus sp.           genus         33636
    ## 511                   Climacograptus sp.           genus         33636
    ## 523                   Climacograptus sp.           genus         33636
    ## 529                   Climacograptus sp.           genus         33636
    ## 534                   Climacograptus sp.           genus         33636
    ## 544                   Climacograptus sp.           genus         33636
    ## 549                   Climacograptus sp.           genus         33636
    ## 553                   Climacograptus sp.           genus         33636
    ## 560                   Climacograptus sp.           genus         33636
    ## 571                   Climacograptus sp.           genus         33636
    ## 579                   Climacograptus sp.           genus         33636
    ## 586                   Climacograptus sp.           genus         33636
    ## 587                   Climacograptus sp.           genus         33636
    ## 627                   Climacograptus sp.           genus         33636
    ## 634                   Climacograptus sp.           genus         33636
    ## 641                   Climacograptus sp.           genus         33636
    ## 659                   Climacograptus sp.           genus         33636
    ## 665                   Climacograptus sp.           genus         33636
    ## 666                   Climacograptus sp.           genus         33636
    ## 670                   Climacograptus sp.           genus         33636
    ## 698                   Climacograptus sp.           genus         33636
    ## 706                   Climacograptus sp.           genus         33636
    ## 725                   Climacograptus sp.           genus         33636
    ## 729                   Climacograptus sp.           genus         33636
    ## 734                   Climacograptus sp.           genus         33636
    ## 738                   Climacograptus sp.           genus         33636
    ## 741                   Climacograptus sp.           genus         33636
    ## 746                   Climacograptus sp.           genus         33636
    ## 759                   Climacograptus sp.           genus         33636
    ## 791                   Climacograptus sp.           genus         33636
    ## 795                   Climacograptus sp.           genus         33636
    ## 808                   Climacograptus sp.           genus         33636
    ## 813                   Climacograptus sp.           genus         33636
    ## 819                   Climacograptus sp.           genus         33636
    ## 837                   Climacograptus sp.           genus         33636
    ## 865                   Climacograptus sp.           genus         33636
    ## 887                   Climacograptus sp.           genus         33636
    ## 891                   Climacograptus sp.           genus         33636
    ## 918                   Climacograptus sp.           genus         33636
    ## 920                   Climacograptus sp.           genus         33636
    ## 923                   Climacograptus sp.           genus         33636
    ## 929                   Climacograptus sp.           genus         33636
    ## 933                   Climacograptus sp.           genus         33636
    ## 949                   Climacograptus sp.           genus         33636
    ## 960                   Climacograptus sp.           genus         33636
    ## 968                   Climacograptus sp.           genus         33636
    ## 1000                  Climacograptus sp.           genus         33636
    ## 1003                  Climacograptus sp.           genus         33636
    ## 1012                  Climacograptus sp.           genus         33636
    ## 1016                  Climacograptus sp.           genus         33636
    ## 1027                  Climacograptus sp.           genus         33636
    ## 1059                  Climacograptus sp.           genus         33636
    ## 1086                  Climacograptus sp.           genus         33636
    ## 1090                  Climacograptus sp.           genus         33636
    ## 1101                  Climacograptus sp.           genus         33636
    ## 1130                  Climacograptus sp.           genus         33636
    ## 1138                  Climacograptus sp.           genus         33636
    ## 1163                  Climacograptus sp.           genus         33636
    ## 1166                  Climacograptus sp.           genus         33636
    ## 1213                  Climacograptus sp.           genus         33636
    ## 1215                  Climacograptus sp.           genus         33636
    ## 1221                  Climacograptus sp.           genus         33636
    ## 1229                  Climacograptus sp.           genus         33636
    ## 1247                  Climacograptus sp.           genus         33636
    ## 1252                  Climacograptus sp.           genus         33636
    ## 1273                  Climacograptus sp.           genus         33636
    ## 1285                  Climacograptus sp.           genus         33636
    ## 1290                  Climacograptus sp.           genus         33636
    ## 1305                  Climacograptus sp.           genus         33636
    ## 1309                  Climacograptus sp.           genus         33636
    ## 1315               Diplograptidae indet.          family        150197
    ## 1316      Climacograptus miserabilis cf.         species         33636
    ## 1317                  Climacograptus sp.           genus         33636
    ## 1360                  Climacograptus sp.           genus         33636
    ## 1394                  Climacograptus sp.           genus         33636
    ## 1412                  Climacograptus sp.           genus         33636
    ## 1416                Climacograptus " sp.           genus         33636
    ## 1432                  Climacograptus sp.           genus         33636
    ## 1465                  Climacograptus sp.           genus         33636
    ## 1473                  Climacograptus sp.           genus         33636
    ## 1554 Climacograptus rectangulares-medius         species         33636
    ## 1556 Climacograptus rectangularis-medius         species         33636
    ## 1566                  Climacograptus sp.           genus         33636
    ## 1568 Climacograptus C. rectangularis cf.         species         33636
    ## 1569            Climacograptus typicalis         species         33636
    ## 1571              Climacograptus pumilis         species         33636
    ## 1573          Climacograptus tubuliferus         species         33636
    ## 1574             Climacograptus caudatus         species         33636
    ## 1575            Climacograptus innotatus         species         33636
    ## 1579             Climacograptus caudatus         species         33636
    ## 1580            Climacograptus innotatus         species         33636
    ## 1581          Climacograptus minimus cf.         species         33636
    ## 1582          Climacograptus tubuliferus         species         33636
    ## 1586          Climacograptus uncinatus ?         species         33636
    ## 1590             Climacograptus angustus         species         33636
    ## 1591          Climacograptus miserabilis         species         33636
    ## 1596             Climacograptus angustus         species         33636
    ## 1597               Climacograptus medius         species         33636
    ## 1599        Climacograptus rectangularis         species         33636
    ## 1600             Climacograptus angustus         species         33636
    ## 1601               Climacograptus medius         species         33636
    ## 1605        Climacograptus rectangularis         species         33636
    ## 1606             Climacograptus balticus         species         33636
    ## 1612        Climacograptus rectangularis         species         33636
    ## 1613           Climacograptus scalaris ?         species        316364
    ## 1637           Climacograptus scalaris ?         species        316364
    ## 1648           Climacograptus scalaris ?         species        316364
    ## 1839           Climacograptus medius cf.         species         33636
    ## 2120                  Climacograptus sp.           genus         33636
    ## 2124                  Climacograptus sp.           genus         33636
    ## 2128                  Climacograptus sp.           genus         33636
    ## 2140                  Climacograptus sp.           genus         33636
    ## 2150                  Climacograptus sp.           genus         33636
    ## 2166                  Climacograptus sp.           genus         33636
    ## 2173                  Climacograptus sp.           genus         33636
    ## 2185                  Climacograptus sp.           genus         33636
    ## 2192                  Climacograptus sp.           genus         33636
    ## 2199                  Climacograptus sp.           genus         33636
    ## 2202                  Climacograptus sp.           genus         33636
    ## 2211                  Climacograptus sp.           genus         33636
    ## 2214                  Climacograptus sp.           genus         33636
    ## 2224                  Climacograptus sp.           genus         33636
    ## 2234                  Climacograptus sp.           genus         33636
    ## 2239                  Climacograptus sp.           genus         33636
    ## 2246                  Climacograptus sp.           genus         33636
    ## 2256                  Climacograptus sp.           genus         33636
    ## 2291                  Climacograptus sp.           genus         33636
    ## 2317                  Climacograptus sp.           genus         33636
    ## 2325                  Climacograptus sp.           genus         33636
    ## 2328                  Climacograptus sp.           genus         33636
    ## 2341                  Climacograptus sp.           genus         33636
    ## 2347                  Climacograptus sp.           genus         33636
    ## 2362                  Climacograptus sp.           genus         33636
    ## 2368                  Climacograptus sp.           genus         33636
    ## 2376                  Climacograptus sp.           genus         33636
    ## 2379                  Climacograptus sp.           genus         33636
    ## 2399             Climacograptus bicornis         species        306375
    ## 2400               Climacograptus inuiti         species         33636
    ## 2413             Climacograptus venustus         species         33636
    ## 2424            Climacograptus typicalis         species         33636
    ## 2425            Climacograptus dorotheus         species         33636
    ## 2437        Climacograptus scalaris aff.         species        316364
    ## 2456                  Climacograptus sp.           genus         33636
    ## 2459        Climacograptus rectangularis         species         33636
    ## 2463               Climacograptus medius         species         33636
    ## 2464        Climacograptus rectangularis         species         33636
    ## 2466               Climacograptus medius         species         33636
    ## 2501            Climacograptus innotatus         species         33636
    ## 2502    Climacograptus rectangularis cf.         species         33636
    ## 2505          Climacograptus minutus cf.         species         33636
    ## 2507            Climacograptus typicalis         species         33636
    ## 2508          Climacograptus spiniferous         species         33636
    ## 2518             Climacograptus angustus         species         33636
    ## 2520             Climacograptus venustus         species         33636
    ## 2521                  Climacograptus sp.           genus         33636
    ## 2525             Climacograptus supernus         species         33636
    ## 2526             Climacograptus hvalross         species         33636
    ## 2527             Climacograptus hastatus         species         33636
    ## 2528     Climacograptus raricaudatus cf.         species         33636
    ## 2530             Climacograptus scalaris         species        316364
    ## 2562         Climacograptus bicornis cf.         species        306375
    ## 2565         Climacograptus bicornis cf.         species        306375
    ## 2585                  Climacograptus sp.           genus         33636
    ## 2587                  Climacograptus sp.           genus         33636
    ## 2593                  Climacograptus sp.           genus         33636
    ## 2644                  Climacograptus sp.           genus         33636
    ## 2646                  Climacograptus sp.           genus         33636
    ## 2661                  Climacograptus sp.           genus         33636
    ## 2706               Diplograptidae indet.          family        150197
    ## 2707            Climacograptus innotatus         species         33636
    ## 2708            Climacograptus innotatus         species         33636
    ## 2710                  Climacograptus sp.           genus         33636
    ## 2755                  Climacograptus sp.           genus         33636
    ## 2793                  Climacograptus sp.           genus         33636
    ## 2797              Climacograptus aqualis         species         33636
    ## 2798           Climacograptus prolificus         species         33636
    ## 2799            Climacograptus typicalis         species         33636
    ## 2804            Climacograptus typicalis         species         33636
    ## 2806            Climacograptus typicalis         species         33636
    ## 2807            Climacograptus typicalis         species         33636
    ## 2809           Climacograptus prolificus         species         33636
    ## 2810            Climacograptus rougensis         species         33636
    ## 2884             Climacograptus scalaris         species        316364
    ## 2891                  Climacograptus sp.           genus         33636
    ## 2892        Climacograptus bohemicus cf.         species         33636
    ## 2893         Climacograptus yangtseensis         species         33636
    ## 2934         Climacograptus scalaris cf.         species        316364
    ## 2935    Climacograptus rectangularis cf.         species         33636
    ## 2943               Climacograptus medius         species         33636
    ## 2948             Climacograptus scalaris         species        316364
    ## 3021         Climacograptus scalaris cf.         species        316364
    ## 3108          Climacograptus minutus cf.         species         33636
    ## 3110             Climacograptus angustus         species         33636
    ## 3116                  Climacograptus sp.           genus         33636
    ## 3127             Climacograptus angustus         species         33636
    ## 3128              Climacograptus minutus         species         33636
    ## 3129    Climacograptus rectangularis cf.         species         33636
    ## 3148         Climacograptus yangtzeensis         species         33636
    ## 3149               Climacograptus medius         species         33636
    ## 3173             Climacograptus scalaris         species        316364
    ## 3182               Climacograptus medius         species         33636
    ## 3199           Climacograptus mirnyensis         species         33636
    ## 3200             Climacograptus angustus         species         33636
    ## 3202                  Climacograptus sp.           genus         33636
    ## 3246             Climacograptus scalaris         species        316364
    ## 3248        Climacograptus rectangularis         species         33636
    ## 3276                  Climacograptus sp.           genus         33636
    ## 3290        Climacograptus tangshanensis         species         33636
    ## 3318                  Climacograptus sp.           genus         33636
    ## 3353      Climacograptus yangtzensis cf.         species         33636
    ## 3358                  Climacograptus sp.           genus         33636
    ## 3366             Climacograptus supernus         species         33636
    ## 3377                  Climacograptus sp.           genus         33636
    ## 3386        Climacograptus rectangulatus         species         33636
    ## 3403            Climacograptus typicalis         species         33636
    ## 3462                  Climacograptus sp.           genus         33636
    ## 3473                  Climacograptus sp.           genus         33636
    ## 3479                  Climacograptus sp.           genus         33636
    ## 3485                  Climacograptus sp.           genus         33636
    ## 3530     Climacograptus tubuliferus aff.         species         33636
    ## 3541                  Climacograptus sp.           genus         33636
    ## 3545                  Climacograptus sp.           genus         33636
    ## 3677               Climacograptus brevis         species         33636
    ## 3842                  Climacograptus sp.           genus         33636
    ## 3847               Diplograptidae indet.          family        150197
    ## 3848               Diplograptidae indet.          family        150197
    ## 3849               Diplograptidae indet.          family        150197
    ## 3857               Diplograptidae indet.          family        150197
    ## 3859             Climacograptus antiquus         species         33636
    ## 3866             Climacograptus antiquus         species         33636
    ## 3867                  Climacograptus sp.           genus         33636
    ## 3894             Climacograptus antiquus         species         33636
    ## 3903             Climacograptus antiquus         species         33636
    ## 3912             Climacograptus antiquus         species         33636
    ## 3919                  Climacograptus sp.           genus         33636
    ## 3937               Diplograptidae indet.          family        150197
    ## 3941                  Climacograptus sp.           genus         33636
    ## 3942             Climacograptus antiquus         species         33636
    ## 3949         Climacograptus antiquus cf.         species         33636
    ## 3956         Climacograptus antiquus cf.         species         33636
    ## 3968             Climacograptus antiquus         species         33636
    ## 3979                  Climacograptus sp.           genus         33636
    ## 3983             Climacograptus antiquus         species         33636
    ## 3998         Climacograptus antiquus cf.         species         33636
    ## 4011             Climacograptus antiquus         species         33636
    ## 4023             Climacograptus angustus         species         33636
    ## 4038                  Climacograptus sp.           genus         33636
    ## 4041           Climacograptus angustatus         species         33636
    ## 4046                  Climacograptus sp.           genus         33636
    ## 4051                Parareteograptus sp.           genus        270338
    ## 4061          Climacograptus minimus cf.         species         33636
    ## 4062           Climacograptus styloideus         species         33636
    ## 4067          Climacograptus minimus cf.         species         33636
    ## 4072                  Climacograptus sp.           genus         33636
    ## 4075                  Climacograptus sp.           genus         33636
    ## 4096                  Climacograptus sp.           genus         33636
    ## 4097            Climacograptus typicalis         species         33636
    ## 4099            Climacograptus typicalis         species         33636
    ## 4101                  Climacograptus sp.           genus         33636
    ## 4102            Climacograptus typicalis         species         33636
    ## 4104               Climacograptus brevis         species         33636
    ## 4110                  Climacograptus sp.           genus         33636
    ## 4113         Climacograptus scharenbergi         species         33636
    ## 4115                  Climacograptus sp.           genus         33636
    ## 4138                  Climacograptus sp.           genus         33636
    ## 4141              Climacograptus minimus         species         33636
    ## 4142           Climacograptus styloideus         species         33636
    ## 4150          Climacograptus tridentatus         species         33636
    ## 4166             Climacograptus bicornis         species        306375
    ## 4167                  Climacograptus sp.           genus         33636
    ## 4256         Climacograptus riddellensis         species         33636
    ## 4257                  Climacograptus sp.           genus         33636
    ## 4266         Climacograptus riddellensis         species         33636
    ## 4267     Climacograptus scharenbergi cf.         species         33636
    ## 4286                  Climacograptus sp.           genus         33636
    ## 4292     Climacograptus phyllophorus cf.         species         33636
    ## 4293     Climacograptus phyllophorus cf.         species         33636
    ## 4302                Climacograptus latus         species         33636
    ## 4303                Climacograptus latus         species         33636
    ## 4305                Climacograptus latus         species         33636
    ## 4309              Climacograptus pungens         species         33636
    ## 4316                  Climacograptus sp.           genus         33636
    ## 4317                  Climacograptus sp.           genus         33636
    ## 4320             Climacograptus bicornis         species        306375
    ## 4325             Climacograptus bicornis         species        306375
    ## 4332             Climacograptus bicornis         species        306375
    ## 4333          Climacograptus eximius cf.         species         33636
    ## 4340                  Climacograptus sp.           genus         33636
    ## 4345                  Climacograptus sp.           genus         33636
    ## 4350                  Climacograptus sp.           genus         33636
    ## 4353          Climacograptus hughesi cf.         species         33636
    ## 4354         Climacograptus scalaris cf.         species        316364
    ## 4355                  Climacograptus sp.           genus         33636
    ## 4358                  Climacograptus sp.           genus         33636
    ## 4366                  Climacograptus sp.           genus         33636
    ## 4379                  Climacograptus sp.           genus         33636
    ## 4386                  Climacograptus sp.           genus         33636
    ## 4391                  Climacograptus sp.           genus         33636
    ## 4402        Climacograptus antiquus aff.         species         33636
    ## 4413     Climacograptus phyllophorus cf.         species         33636
    ## 4414                  Climacograptus sp.           genus         33636
    ## 4436                  Climacograptus sp.           genus         33636
    ## 4444                  Climacograptus sp.           genus         33636
    ## 4498                  Climacograptus sp.           genus         33636
    ## 4501                  Climacograptus sp.           genus         33636
    ## 4516             Climacograptus bicornis         species        306375
    ## 4522               Climacograptus brevis         species         33636
    ## 4662                  Climacograptus sp.           genus         33636
    ## 4667                  Climacograptus sp.           genus         33636
    ## 4671                  Climacograptus sp.           genus         33636
    ## 4673                  Climacograptus sp.           genus         33636
    ## 4685             Climacograptus bicornis         species        306375
    ## 4686               Climacograptus brevis         species         33636
    ## 4695             Climacograptus bicornis         species        306375
    ## 4703             Climacograptus bicornis         species        306375
    ## 4713             Climacograptus bicornis         species        306375
    ## 4725             Climacograptus bicornis         species        306375
    ## 4726         Climacograptus riddellensis         species         33636
    ## 4748                  Climacograptus sp.           genus         33636
    ## 4756                  Climacograptus sp.           genus         33636
    ## 4765                  Climacograptus sp.           genus         33636
    ## 4773             Climacograptus bicornis         species        306375
    ## 4774             Climacograptus bicornis         species        306375
    ## 4775         Climacograptus bicornis cf.         species        306375
    ## 4776     Climacograptus raricaudatus cf.         species         33636
    ## 4777      Climacograptus tubuliferus cf.         species         33636
    ## 4780                  Climacograptus sp.           genus         33636
    ## 4781                  Climacograptus sp.           genus         33636
    ## 4782                  Climacograptus sp.           genus         33636
    ## 4816             Climacograptus caudatus         species         33636
    ## 4817             Climacograptus caudatus         species         33636
    ## 4818             Climacograptus caudatus         species         33636
    ## 4819             Climacograptus caudatus         species         33636
    ## 4820            Climacograptus innotatus         species         33636
    ## 4821            Climacograptus innotatus         species         33636
    ## 4822      Climacograptus mohawkensis cf.         species         33636
    ## 4823      Climacograptus mohawkensis cf.         species         33636
    ## 4824          Climacograptus tubuliferus         species         33636
    ## 4825          Climacograptus tubuliferus         species         33636
    ## 4826          Climacograptus tubuliferus         species         33636
    ## 4827          Climacograptus tubuliferus         species         33636
    ## 4828          Climacograptus tubuliferus         species         33636
    ## 4829          Climacograptus tubuliferus         species         33636
    ## 4830          Climacograptus tubuliferus         species         33636
    ## 4831          Climacograptus tubuliferus         species         33636
    ## 4833                  Climacograptus sp.           genus         33636
    ## 4834                  Climacograptus sp.           genus         33636
    ## 4835                  Climacograptus sp.           genus         33636
    ## 4836                  Climacograptus sp.           genus         33636
    ## 4837                  Climacograptus sp.           genus         33636
    ## 4838                  Climacograptus sp.           genus         33636
    ## 4839                  Climacograptus sp.           genus         33636
    ## 4883           Climacograptus hastatus ?         species         33636
    ## 4884             Climacograptus hastatus         species         33636
    ## 4885             Climacograptus hastatus         species         33636
    ## 4886             Climacograptus hastatus         species         33636
    ## 4887             Climacograptus hastatus         species         33636
    ## 4888             Climacograptus hastatus         species         33636
    ## 4889          Climacograptus longispinus         species         33636
    ## 4890          Climacograptus longispinus         species         33636
    ## 4891          Climacograptus longispinus         species         33636
    ## 4892          Climacograptus longispinus         species         33636
    ## 4893          Climacograptus longispinus         species         33636
    ## 4899      Climacograptus mohawkensis cf.         species         33636
    ## 4900      Climacograptus mohawkensis cf.         species         33636
    ## 4901      Climacograptus mohawkensis cf.         species         33636
    ## 4902      Climacograptus mohawkensis cf.         species         33636
    ## 4903            Climacograptus pacificus         species         33636
    ## 4904            Climacograptus pacificus         species         33636
    ## 4905            Climacograptus pacificus         species         33636
    ## 4906      Climacograptus tabuliferus cf.         species         33636
    ## 4907      Climacograptus tabuliferus cf.         species         33636
    ## 4908      Climacograptus tabuliferus cf.         species         33636
    ## 4909      Climacograptus tabuliferus cf.         species         33636
    ## 4910      Climacograptus tabuliferus cf.         species         33636
    ## 4911            Climacograptus uncinatus         species         33636
    ## 4912            Climacograptus uncinatus         species         33636
    ## 4913            Climacograptus uncinatus         species         33636
    ## 4914            Climacograptus uncinatus         species         33636
    ## 4915            Climacograptus uncinatus         species         33636
    ## 4916            Climacograptus uncinatus         species         33636
    ## 4917       Climacograptus sp. A informal           genus         33636
    ## 4918       Climacograptus sp. A informal           genus         33636
    ## 4919       Climacograptus sp. A informal           genus         33636
    ## 4920       Climacograptus sp. A informal           genus         33636
    ## 4921       Climacograptus sp. A informal           genus         33636
    ## 4923       Climacograptus sp. A informal           genus         33636
    ## 4924       Climacograptus sp. A informal           genus         33636
    ## 4925           Climacograptus latus aff.         species         33636
    ## 4926                  Climacograptus sp.           genus         33636
    ## 4927                  Climacograptus sp.           genus         33636
    ## 4928                  Climacograptus sp.           genus         33636
    ## 4929                  Climacograptus sp.           genus         33636
    ## 4962         Climacograptus scalaris cf.         species        316364
    ## 4963         Climacograptus scalaris cf.         species        316364
    ## 4964                  Climacograptus sp.           genus         33636
    ## 5102           Climacograptus medius cf.         species         33636
    ## 5103             Climacograptus trifilis         species         33636
    ## 5106           Climacograptus medius cf.         species         33636
    ## 5110           Climacograptus medius cf.         species         33636
    ## 5114            Climacograptus innotatus         species         33636
    ## 5115             Climacograptus scalaris         species        316364
    ## 5126            Climacograptus indivisus         species         33636
    ## 5127            Climacograptus innotatus         species         33636
    ## 5128           Climacograptus medius cf.         species         33636
    ## 5129            Climacograptus minutus ?         species         33636
    ## 5130    Climacograptus rectangularis cf.         species         33636
    ## 5131        Climacograptus rectangularis         species         33636
    ## 5132             Climacograptus scalaris         species        316364
    ## 5150            Climacograptus innotatus         species         33636
    ## 5151           Climacograptus medius cf.         species         33636
    ## 5152    Climacograptus rectangularis cf.         species         33636
    ## 5153        Climacograptus rectangularis         species         33636
    ## 5154             Climacograptus scalaris         species        316364
    ## 5155             Climacograptus trifilis         species         33636
    ## 5167           Climacograptus stenotelus         species         33636
    ## 5176               Climacograptus medius         species         33636
    ## 5177    Climacograptus rectangularis cf.         species         33636
    ## 5195           Climacograptus medius cf.         species         33636
    ## 5204             Climacograptus scalaris         species        316364
    ## 5205        Climacograptus rectangularis         species         33636
    ## 5248               Anticostia tenuissima         species        270341
    ## 5249                     Anticostia lata         species        270341
    ## 5250           Anticostia thorsteinssoni         species        270341
    ## 5251               Anticostia fastigiata         species        270341
    ## 5253             Climacograptus hastatus         species         33636
    ## 5256           Parareteograptus sinensis         species        270338
    ## 5260            Rectograptus abbreviatus         species        270339
    ## 5261                     Anticostia lata         species        270341
    ## 5262                Anticostia fastigata         species        270341
    ## 5263               Anticostia tenuissima         species        270341
    ## 5265             Climacograptus hastatus         species         33636
    ## 5268           Parareteograptus sinensis         species        270338
    ## 5270            Rectograptus abbreviatus         species        270339
    ## 5275                Anticostia festigata         species        270341
    ## 5277             Climacograptus hastatus         species         33636
    ## 5281           Parareteograptus sinensis         species        270338
    ## 5286                     Anticostia lata         species        270341
    ## 5287                Anticostia fastigata         species        270341
    ## 5289             Climacograptus hastatus         species         33636
    ## 5293           Parareteograptus sinensis         species        270338
    ## 5298                     Anticostia lata         species        270341
    ## 5299                     Anticostia lata         species        270341
    ## 5300                Anticostia fastigata         species        270341
    ## 5301                Anticostia fastigata         species        270341
    ## 5302                Anticostia fastigata         species        270341
    ## 5305             Climacograptus hastatus         species         33636
    ## 5306             Climacograptus hastatus         species         33636
    ## 5307             Climacograptus hastatus         species         33636
    ## 5314           Parareteograptus sinensis         species        270338
    ## 5315           Parareteograptus sinensis         species        270338
    ## 5319               Anticostia tenuissima         species        270341
    ## 5320               Anticostia tenuissima         species        270341
    ## 5322            Rectograptus abbreviatus         species        270339
    ## 5323            Rectograptus abbreviatus         species        270339
    ## 5326                Anticostia uniformis         species        270341
    ## 5327                Anticostia uniformis         species        270341
    ## 5330             Climacograptus bicornis         species        306375
    ## 5333               Climacograptus brevis         species         33636
    ## 5342                  Climacograptus sp.           genus         33636
    ## 5343               Climacograptus medius         species         33636
    ## 5344             Climacograptus scalaris         species        316364
    ## 5345        Climacograptus rectangularis         species         33636
    ## 5346             Climacograptus trifilis         species         33636
    ## 5347                  Climacograptus sp.           genus         33636
    ## 5353           Climacograptus longespina         species         33636
    ## 5354               Climacograptus medius         species         33636
    ## 5355             Climacograptus scalaris         species        316364
    ## 5363           Climacograptus longespina         species         33636
    ## 5364               Climacograptus medius         species         33636
    ## 5365             Climacograptus scalaris         species        316364
    ## 5385             Climacograptus scalaris         species        316364
    ## 5486                     Anticostia lata         species        270341
    ## 5487                Anticostia fastigata         species        270341
    ## 5488               Anticostia tenuissima         species        270341
    ## 5490             Climacograptus hastatus         species         33636
    ## 5495           Parareteograptus sinensis         species        270338
    ## 5496            Rectograptus abbreviatus         species        270339
    ## 5506                     Anticostia lata         species        270341
    ## 5508             Climacograptus hastatus         species         33636
    ## 5513           Parareteograptus sinensis         species        270338
    ## 5515            Rectograptus abbreviatus         species        270339
    ## 5518                Anticostia uniformis         species        270341
    ## 5523             Parareteograptus parvus         species        270338
    ## 5524                     Anticostia lata         species        270341
    ## 5525             Climacograptus hastatus         species         33636
    ## 5530           Parareteograptus sinensis         species        270338
    ## 5532            Rectograptus abbreviatus         species        270339
    ## 5538                Anticostia uniformis         species        270341
    ## 5544             Parareteograptus parvus         species        270338
    ## 5547           Parareteograptus turgidus         species        270338
    ## 5548                     Anticostia lata         species        270341
    ## 5549             Climacograptus hastatus         species         33636
    ## 5554            Rectograptus abbreviatus         species        270339
    ## 5559                Anticostia uniformis         species        270341
    ## 5563             Parareteograptus parvus         species        270338
    ## 5565           Parareteograptus turgidus         species        270338
    ## 5567                     Anticostia lata         species        270341
    ## 5568             Climacograptus hastatus         species         33636
    ## 5573           Parareteograptus sinensis         species        270338
    ## 5575            Rectograptus abbreviatus         species        270339
    ## 5585              Anticostia macgregorae         species        270341
    ## 5586                     Anticostia lata         species        270341
    ## 5587                Anticostia fastigata         species        270341
    ## 5588             Climacograptus hastatus         species         33636
    ## 5593            Rectograptus abbreviatus         species        270339
    ## 5598                     Anticostia lata         species        270341
    ## 5599             Climacograptus hastatus         species         33636
    ## 5602            Rectograptus abbreviatus         species        270339
    ## 5606                     Anticostia lata         species        270341
    ## 5607             Climacograptus hastatus         species         33636
    ## 5610           Parareteograptus sinensis         species        270338
    ## 5611            Rectograptus abbreviatus         species        270339
    ## 5613                Anticostia uniformis         species        270341
    ## 5616                     Anticostia lata         species        270341
    ## 5617                Anticostia fastigata         species        270341
    ## 5621            Rectograptus abbreviatus         species        270339
    ## 5625                Anticostia uniformis         species        270341
    ## 5631                     Anticostia lata         species        270341
    ## 5632                Anticostia fastigata         species        270341
    ## 5633             Climacograptus hastatus         species         33636
    ## 5637            Rectograptus abbreviatus         species        270339
    ## 5641                Anticostia uniformis         species        270341
    ## 5646              Anticostia macgregorae         species        270341
    ## 5670            Rectograptus abbreviatus         species        270339
    ## 5673                Anticostia uniformis         species        270341
    ## 5719             Climacograptus hastatus         species         33636
    ## 5724           Parareteograptus sinensis         species        270338
    ## 5726            Rectograptus abbreviatus         species        270339
    ## 5727             Climacograptus hastatus         species         33636
    ## 5731            Rectograptus abbreviatus         species        270339
    ## 5732                     Anticostia lata         species        270341
    ## 5735             Climacograptus hastatus         species         33636
    ## 5740           Parareteograptus sinensis         species        270338
    ## 5742            Rectograptus abbreviatus         species        270339
    ## 5743                     Anticostia lata         species        270341
    ## 5745               Anticostia tenuissima         species        270341
    ## 5747             Parareteograptus parvus         species        270338
    ## 5748             Climacograptus hastatus         species         33636
    ## 5752           Parareteograptus sinensis         species        270338
    ## 5754            Rectograptus abbreviatus         species        270339
    ## 5760             Climacograptus hastatus         species         33636
    ## 5764           Parareteograptus sinensis         species        270338
    ## 5766            Rectograptus abbreviatus         species        270339
    ## 5776             Climacograptus hastatus         species         33636
    ## 5783            Rectograptus abbreviatus         species        270339
    ## 5843            Rectograptus abbreviatus         species        270339
    ## 5845        Climacograptus indivisus cf.         species         33636
    ## 5871             Climacograptus scalaris         species        316364
    ## 5886           Climacograptus styloideus         species         33636
    ## 5892             Climacograptus antiquus         species         33636
    ## 5896             Climacograptus scalaris         species        316364
    ##             taxonomic_reason           accepted_name accepted_rank
    ## 32                      <NA>          Climacograptus         genus
    ## 39                      <NA>          Climacograptus         genus
    ## 56                      <NA>          Climacograptus         genus
    ## 58                      <NA>          Climacograptus         genus
    ## 66                      <NA>          Climacograptus         genus
    ## 74                      <NA>          Climacograptus         genus
    ## 77                      <NA>          Climacograptus         genus
    ## 83                      <NA>          Climacograptus         genus
    ## 89                      <NA>          Climacograptus         genus
    ## 94                      <NA>          Climacograptus         genus
    ## 105                     <NA>          Climacograptus         genus
    ## 110                     <NA>          Climacograptus         genus
    ## 115                     <NA>          Climacograptus         genus
    ## 117                     <NA>          Climacograptus         genus
    ## 120                     <NA>          Climacograptus         genus
    ## 122                     <NA>          Climacograptus         genus
    ## 128                     <NA>          Climacograptus         genus
    ## 131                     <NA>          Climacograptus         genus
    ## 152                     <NA>          Climacograptus         genus
    ## 156                     <NA>          Climacograptus         genus
    ## 181                     <NA>          Climacograptus         genus
    ## 192                     <NA>          Climacograptus         genus
    ## 194                     <NA>          Climacograptus         genus
    ## 214                     <NA>          Climacograptus         genus
    ## 226                     <NA>          Climacograptus         genus
    ## 233                     <NA> Climacograptus scalaris       species
    ## 234  taxon not fully entered          Climacograptus         genus
    ## 236                     <NA> Climacograptus scalaris       species
    ## 237  taxon not fully entered          Climacograptus         genus
    ## 257                     <NA>          Climacograptus         genus
    ## 259                     <NA>          Climacograptus         genus
    ## 261                     <NA>          Climacograptus         genus
    ## 264                     <NA>          Climacograptus         genus
    ## 267                     <NA>          Climacograptus         genus
    ## 269                     <NA>          Climacograptus         genus
    ## 273                     <NA>          Climacograptus         genus
    ## 276                     <NA>          Climacograptus         genus
    ## 283                     <NA>          Climacograptus         genus
    ## 294                     <NA>          Climacograptus         genus
    ## 298                     <NA>          Climacograptus         genus
    ## 303                     <NA>          Climacograptus         genus
    ## 312                     <NA>          Climacograptus         genus
    ## 400                     <NA>          Climacograptus         genus
    ## 411                     <NA>          Climacograptus         genus
    ## 415                     <NA>            Rectograptus         genus
    ## 416                     <NA>          Climacograptus         genus
    ## 418                     <NA>            Rectograptus         genus
    ## 422                     <NA>            Rectograptus         genus
    ## 436  taxon not fully entered          Climacograptus         genus
    ## 444                     <NA>          Climacograptus         genus
    ## 472                     <NA>          Climacograptus         genus
    ## 482                     <NA>          Climacograptus         genus
    ## 489                     <NA>          Climacograptus         genus
    ## 493                     <NA>          Climacograptus         genus
    ## 502                     <NA>          Climacograptus         genus
    ## 511                     <NA>          Climacograptus         genus
    ## 523                     <NA>          Climacograptus         genus
    ## 529                     <NA>          Climacograptus         genus
    ## 534                     <NA>          Climacograptus         genus
    ## 544                     <NA>          Climacograptus         genus
    ## 549                     <NA>          Climacograptus         genus
    ## 553                     <NA>          Climacograptus         genus
    ## 560                     <NA>          Climacograptus         genus
    ## 571                     <NA>          Climacograptus         genus
    ## 579                     <NA>          Climacograptus         genus
    ## 586                     <NA>          Climacograptus         genus
    ## 587                     <NA>          Climacograptus         genus
    ## 627                     <NA>          Climacograptus         genus
    ## 634                     <NA>          Climacograptus         genus
    ## 641                     <NA>          Climacograptus         genus
    ## 659                     <NA>          Climacograptus         genus
    ## 665                     <NA>          Climacograptus         genus
    ## 666                     <NA>          Climacograptus         genus
    ## 670                     <NA>          Climacograptus         genus
    ## 698                     <NA>          Climacograptus         genus
    ## 706                     <NA>          Climacograptus         genus
    ## 725                     <NA>          Climacograptus         genus
    ## 729                     <NA>          Climacograptus         genus
    ## 734                     <NA>          Climacograptus         genus
    ## 738                     <NA>          Climacograptus         genus
    ## 741                     <NA>          Climacograptus         genus
    ## 746                     <NA>          Climacograptus         genus
    ## 759                     <NA>          Climacograptus         genus
    ## 791                     <NA>          Climacograptus         genus
    ## 795                     <NA>          Climacograptus         genus
    ## 808                     <NA>          Climacograptus         genus
    ## 813                     <NA>          Climacograptus         genus
    ## 819                     <NA>          Climacograptus         genus
    ## 837                     <NA>          Climacograptus         genus
    ## 865                     <NA>          Climacograptus         genus
    ## 887                     <NA>          Climacograptus         genus
    ## 891                     <NA>          Climacograptus         genus
    ## 918                     <NA>          Climacograptus         genus
    ## 920                     <NA>          Climacograptus         genus
    ## 923                     <NA>          Climacograptus         genus
    ## 929                     <NA>          Climacograptus         genus
    ## 933                     <NA>          Climacograptus         genus
    ## 949                     <NA>          Climacograptus         genus
    ## 960                     <NA>          Climacograptus         genus
    ## 968                     <NA>          Climacograptus         genus
    ## 1000                    <NA>          Climacograptus         genus
    ## 1003                    <NA>          Climacograptus         genus
    ## 1012                    <NA>          Climacograptus         genus
    ## 1016                    <NA>          Climacograptus         genus
    ## 1027                    <NA>          Climacograptus         genus
    ## 1059                    <NA>          Climacograptus         genus
    ## 1086                    <NA>          Climacograptus         genus
    ## 1090                    <NA>          Climacograptus         genus
    ## 1101                    <NA>          Climacograptus         genus
    ## 1130                    <NA>          Climacograptus         genus
    ## 1138                    <NA>          Climacograptus         genus
    ## 1163                    <NA>          Climacograptus         genus
    ## 1166                    <NA>          Climacograptus         genus
    ## 1213                    <NA>          Climacograptus         genus
    ## 1215                    <NA>          Climacograptus         genus
    ## 1221                    <NA>          Climacograptus         genus
    ## 1229                    <NA>          Climacograptus         genus
    ## 1247                    <NA>          Climacograptus         genus
    ## 1252                    <NA>          Climacograptus         genus
    ## 1273                    <NA>          Climacograptus         genus
    ## 1285                    <NA>          Climacograptus         genus
    ## 1290                    <NA>          Climacograptus         genus
    ## 1305                    <NA>          Climacograptus         genus
    ## 1309                    <NA>          Climacograptus         genus
    ## 1315                    <NA>          Diplograptidae        family
    ## 1316 taxon not fully entered          Climacograptus         genus
    ## 1317                    <NA>          Climacograptus         genus
    ## 1360                    <NA>          Climacograptus         genus
    ## 1394                    <NA>          Climacograptus         genus
    ## 1412                    <NA>          Climacograptus         genus
    ## 1416                    <NA>          Climacograptus         genus
    ## 1432                    <NA>          Climacograptus         genus
    ## 1465                    <NA>          Climacograptus         genus
    ## 1473                    <NA>          Climacograptus         genus
    ## 1554 taxon not fully entered          Climacograptus         genus
    ## 1556 taxon not fully entered          Climacograptus         genus
    ## 1566                    <NA>          Climacograptus         genus
    ## 1568 taxon not fully entered          Climacograptus         genus
    ## 1569 taxon not fully entered          Climacograptus         genus
    ## 1571 taxon not fully entered          Climacograptus         genus
    ## 1573 taxon not fully entered          Climacograptus         genus
    ## 1574 taxon not fully entered          Climacograptus         genus
    ## 1575 taxon not fully entered          Climacograptus         genus
    ## 1579 taxon not fully entered          Climacograptus         genus
    ## 1580 taxon not fully entered          Climacograptus         genus
    ## 1581 taxon not fully entered          Climacograptus         genus
    ## 1582 taxon not fully entered          Climacograptus         genus
    ## 1586 taxon not fully entered          Climacograptus         genus
    ## 1590 taxon not fully entered          Climacograptus         genus
    ## 1591 taxon not fully entered          Climacograptus         genus
    ## 1596 taxon not fully entered          Climacograptus         genus
    ## 1597 taxon not fully entered          Climacograptus         genus
    ## 1599 taxon not fully entered          Climacograptus         genus
    ## 1600 taxon not fully entered          Climacograptus         genus
    ## 1601 taxon not fully entered          Climacograptus         genus
    ## 1605 taxon not fully entered          Climacograptus         genus
    ## 1606 taxon not fully entered          Climacograptus         genus
    ## 1612 taxon not fully entered          Climacograptus         genus
    ## 1613                    <NA> Climacograptus scalaris       species
    ## 1637                    <NA> Climacograptus scalaris       species
    ## 1648                    <NA> Climacograptus scalaris       species
    ## 1839 taxon not fully entered          Climacograptus         genus
    ## 2120                    <NA>          Climacograptus         genus
    ## 2124                    <NA>          Climacograptus         genus
    ## 2128                    <NA>          Climacograptus         genus
    ## 2140                    <NA>          Climacograptus         genus
    ## 2150                    <NA>          Climacograptus         genus
    ## 2166                    <NA>          Climacograptus         genus
    ## 2173                    <NA>          Climacograptus         genus
    ## 2185                    <NA>          Climacograptus         genus
    ## 2192                    <NA>          Climacograptus         genus
    ## 2199                    <NA>          Climacograptus         genus
    ## 2202                    <NA>          Climacograptus         genus
    ## 2211                    <NA>          Climacograptus         genus
    ## 2214                    <NA>          Climacograptus         genus
    ## 2224                    <NA>          Climacograptus         genus
    ## 2234                    <NA>          Climacograptus         genus
    ## 2239                    <NA>          Climacograptus         genus
    ## 2246                    <NA>          Climacograptus         genus
    ## 2256                    <NA>          Climacograptus         genus
    ## 2291                    <NA>          Climacograptus         genus
    ## 2317                    <NA>          Climacograptus         genus
    ## 2325                    <NA>          Climacograptus         genus
    ## 2328                    <NA>          Climacograptus         genus
    ## 2341                    <NA>          Climacograptus         genus
    ## 2347                    <NA>          Climacograptus         genus
    ## 2362                    <NA>          Climacograptus         genus
    ## 2368                    <NA>          Climacograptus         genus
    ## 2376                    <NA>          Climacograptus         genus
    ## 2379                    <NA>          Climacograptus         genus
    ## 2399                    <NA> Climacograptus bicornis       species
    ## 2400 taxon not fully entered          Climacograptus         genus
    ## 2413 taxon not fully entered          Climacograptus         genus
    ## 2424 taxon not fully entered          Climacograptus         genus
    ## 2425 taxon not fully entered          Climacograptus         genus
    ## 2437                    <NA> Climacograptus scalaris       species
    ## 2456                    <NA>          Climacograptus         genus
    ## 2459 taxon not fully entered          Climacograptus         genus
    ## 2463 taxon not fully entered          Climacograptus         genus
    ## 2464 taxon not fully entered          Climacograptus         genus
    ## 2466 taxon not fully entered          Climacograptus         genus
    ## 2501 taxon not fully entered          Climacograptus         genus
    ## 2502 taxon not fully entered          Climacograptus         genus
    ## 2505 taxon not fully entered          Climacograptus         genus
    ## 2507 taxon not fully entered          Climacograptus         genus
    ## 2508 taxon not fully entered          Climacograptus         genus
    ## 2518 taxon not fully entered          Climacograptus         genus
    ## 2520 taxon not fully entered          Climacograptus         genus
    ## 2521                    <NA>          Climacograptus         genus
    ## 2525 taxon not fully entered          Climacograptus         genus
    ## 2526 taxon not fully entered          Climacograptus         genus
    ## 2527 taxon not fully entered          Climacograptus         genus
    ## 2528 taxon not fully entered          Climacograptus         genus
    ## 2530                    <NA> Climacograptus scalaris       species
    ## 2562                    <NA> Climacograptus bicornis       species
    ## 2565                    <NA> Climacograptus bicornis       species
    ## 2585                    <NA>          Climacograptus         genus
    ## 2587                    <NA>          Climacograptus         genus
    ## 2593                    <NA>          Climacograptus         genus
    ## 2644                    <NA>          Climacograptus         genus
    ## 2646                    <NA>          Climacograptus         genus
    ## 2661                    <NA>          Climacograptus         genus
    ## 2706                    <NA>          Diplograptidae        family
    ## 2707 taxon not fully entered          Climacograptus         genus
    ## 2708 taxon not fully entered          Climacograptus         genus
    ## 2710                    <NA>          Climacograptus         genus
    ## 2755                    <NA>          Climacograptus         genus
    ## 2793                    <NA>          Climacograptus         genus
    ## 2797 taxon not fully entered          Climacograptus         genus
    ## 2798 taxon not fully entered          Climacograptus         genus
    ## 2799 taxon not fully entered          Climacograptus         genus
    ## 2804 taxon not fully entered          Climacograptus         genus
    ## 2806 taxon not fully entered          Climacograptus         genus
    ## 2807 taxon not fully entered          Climacograptus         genus
    ## 2809 taxon not fully entered          Climacograptus         genus
    ## 2810 taxon not fully entered          Climacograptus         genus
    ## 2884                    <NA> Climacograptus scalaris       species
    ## 2891                    <NA>          Climacograptus         genus
    ## 2892 taxon not fully entered          Climacograptus         genus
    ## 2893 taxon not fully entered          Climacograptus         genus
    ## 2934                    <NA> Climacograptus scalaris       species
    ## 2935 taxon not fully entered          Climacograptus         genus
    ## 2943 taxon not fully entered          Climacograptus         genus
    ## 2948                    <NA> Climacograptus scalaris       species
    ## 3021                    <NA> Climacograptus scalaris       species
    ## 3108 taxon not fully entered          Climacograptus         genus
    ## 3110 taxon not fully entered          Climacograptus         genus
    ## 3116                    <NA>          Climacograptus         genus
    ## 3127 taxon not fully entered          Climacograptus         genus
    ## 3128 taxon not fully entered          Climacograptus         genus
    ## 3129 taxon not fully entered          Climacograptus         genus
    ## 3148 taxon not fully entered          Climacograptus         genus
    ## 3149 taxon not fully entered          Climacograptus         genus
    ## 3173                    <NA> Climacograptus scalaris       species
    ## 3182 taxon not fully entered          Climacograptus         genus
    ## 3199 taxon not fully entered          Climacograptus         genus
    ## 3200 taxon not fully entered          Climacograptus         genus
    ## 3202                    <NA>          Climacograptus         genus
    ## 3246                    <NA> Climacograptus scalaris       species
    ## 3248 taxon not fully entered          Climacograptus         genus
    ## 3276                    <NA>          Climacograptus         genus
    ## 3290 taxon not fully entered          Climacograptus         genus
    ## 3318                    <NA>          Climacograptus         genus
    ## 3353 taxon not fully entered          Climacograptus         genus
    ## 3358                    <NA>          Climacograptus         genus
    ## 3366 taxon not fully entered          Climacograptus         genus
    ## 3377                    <NA>          Climacograptus         genus
    ## 3386 taxon not fully entered          Climacograptus         genus
    ## 3403 taxon not fully entered          Climacograptus         genus
    ## 3462                    <NA>          Climacograptus         genus
    ## 3473                    <NA>          Climacograptus         genus
    ## 3479                    <NA>          Climacograptus         genus
    ## 3485                    <NA>          Climacograptus         genus
    ## 3530 taxon not fully entered          Climacograptus         genus
    ## 3541                    <NA>          Climacograptus         genus
    ## 3545                    <NA>          Climacograptus         genus
    ## 3677 taxon not fully entered          Climacograptus         genus
    ## 3842                    <NA>          Climacograptus         genus
    ## 3847                    <NA>          Diplograptidae        family
    ## 3848                    <NA>          Diplograptidae        family
    ## 3849                    <NA>          Diplograptidae        family
    ## 3857                    <NA>          Diplograptidae        family
    ## 3859 taxon not fully entered          Climacograptus         genus
    ## 3866 taxon not fully entered          Climacograptus         genus
    ## 3867                    <NA>          Climacograptus         genus
    ## 3894 taxon not fully entered          Climacograptus         genus
    ## 3903 taxon not fully entered          Climacograptus         genus
    ## 3912 taxon not fully entered          Climacograptus         genus
    ## 3919                    <NA>          Climacograptus         genus
    ## 3937                    <NA>          Diplograptidae        family
    ## 3941                    <NA>          Climacograptus         genus
    ## 3942 taxon not fully entered          Climacograptus         genus
    ## 3949 taxon not fully entered          Climacograptus         genus
    ## 3956 taxon not fully entered          Climacograptus         genus
    ## 3968 taxon not fully entered          Climacograptus         genus
    ## 3979                    <NA>          Climacograptus         genus
    ## 3983 taxon not fully entered          Climacograptus         genus
    ## 3998 taxon not fully entered          Climacograptus         genus
    ## 4011 taxon not fully entered          Climacograptus         genus
    ## 4023 taxon not fully entered          Climacograptus         genus
    ## 4038                    <NA>          Climacograptus         genus
    ## 4041 taxon not fully entered          Climacograptus         genus
    ## 4046                    <NA>          Climacograptus         genus
    ## 4051                    <NA>        Parareteograptus         genus
    ## 4061 taxon not fully entered          Climacograptus         genus
    ## 4062 taxon not fully entered          Climacograptus         genus
    ## 4067 taxon not fully entered          Climacograptus         genus
    ## 4072                    <NA>          Climacograptus         genus
    ## 4075                    <NA>          Climacograptus         genus
    ## 4096                    <NA>          Climacograptus         genus
    ## 4097 taxon not fully entered          Climacograptus         genus
    ## 4099 taxon not fully entered          Climacograptus         genus
    ## 4101                    <NA>          Climacograptus         genus
    ## 4102 taxon not fully entered          Climacograptus         genus
    ## 4104 taxon not fully entered          Climacograptus         genus
    ## 4110                    <NA>          Climacograptus         genus
    ## 4113 taxon not fully entered          Climacograptus         genus
    ## 4115                    <NA>          Climacograptus         genus
    ## 4138                    <NA>          Climacograptus         genus
    ## 4141 taxon not fully entered          Climacograptus         genus
    ## 4142 taxon not fully entered          Climacograptus         genus
    ## 4150 taxon not fully entered          Climacograptus         genus
    ## 4166                    <NA> Climacograptus bicornis       species
    ## 4167                    <NA>          Climacograptus         genus
    ## 4256 taxon not fully entered          Climacograptus         genus
    ## 4257                    <NA>          Climacograptus         genus
    ## 4266 taxon not fully entered          Climacograptus         genus
    ## 4267 taxon not fully entered          Climacograptus         genus
    ## 4286                    <NA>          Climacograptus         genus
    ## 4292 taxon not fully entered          Climacograptus         genus
    ## 4293 taxon not fully entered          Climacograptus         genus
    ## 4302 taxon not fully entered          Climacograptus         genus
    ## 4303 taxon not fully entered          Climacograptus         genus
    ## 4305 taxon not fully entered          Climacograptus         genus
    ## 4309 taxon not fully entered          Climacograptus         genus
    ## 4316                    <NA>          Climacograptus         genus
    ## 4317                    <NA>          Climacograptus         genus
    ## 4320                    <NA> Climacograptus bicornis       species
    ## 4325                    <NA> Climacograptus bicornis       species
    ## 4332                    <NA> Climacograptus bicornis       species
    ## 4333 taxon not fully entered          Climacograptus         genus
    ## 4340                    <NA>          Climacograptus         genus
    ## 4345                    <NA>          Climacograptus         genus
    ## 4350                    <NA>          Climacograptus         genus
    ## 4353 taxon not fully entered          Climacograptus         genus
    ## 4354                    <NA> Climacograptus scalaris       species
    ## 4355                    <NA>          Climacograptus         genus
    ## 4358                    <NA>          Climacograptus         genus
    ## 4366                    <NA>          Climacograptus         genus
    ## 4379                    <NA>          Climacograptus         genus
    ## 4386                    <NA>          Climacograptus         genus
    ## 4391                    <NA>          Climacograptus         genus
    ## 4402 taxon not fully entered          Climacograptus         genus
    ## 4413 taxon not fully entered          Climacograptus         genus
    ## 4414                    <NA>          Climacograptus         genus
    ## 4436                    <NA>          Climacograptus         genus
    ## 4444                    <NA>          Climacograptus         genus
    ## 4498                    <NA>          Climacograptus         genus
    ## 4501                    <NA>          Climacograptus         genus
    ## 4516                    <NA> Climacograptus bicornis       species
    ## 4522 taxon not fully entered          Climacograptus         genus
    ## 4662                    <NA>          Climacograptus         genus
    ## 4667                    <NA>          Climacograptus         genus
    ## 4671                    <NA>          Climacograptus         genus
    ## 4673                    <NA>          Climacograptus         genus
    ## 4685                    <NA> Climacograptus bicornis       species
    ## 4686 taxon not fully entered          Climacograptus         genus
    ## 4695                    <NA> Climacograptus bicornis       species
    ## 4703                    <NA> Climacograptus bicornis       species
    ## 4713                    <NA> Climacograptus bicornis       species
    ## 4725                    <NA> Climacograptus bicornis       species
    ## 4726 taxon not fully entered          Climacograptus         genus
    ## 4748                    <NA>          Climacograptus         genus
    ## 4756                    <NA>          Climacograptus         genus
    ## 4765                    <NA>          Climacograptus         genus
    ## 4773                    <NA> Climacograptus bicornis       species
    ## 4774                    <NA> Climacograptus bicornis       species
    ## 4775                    <NA> Climacograptus bicornis       species
    ## 4776 taxon not fully entered          Climacograptus         genus
    ## 4777 taxon not fully entered          Climacograptus         genus
    ## 4780                    <NA>          Climacograptus         genus
    ## 4781                    <NA>          Climacograptus         genus
    ## 4782                    <NA>          Climacograptus         genus
    ## 4816 taxon not fully entered          Climacograptus         genus
    ## 4817 taxon not fully entered          Climacograptus         genus
    ## 4818 taxon not fully entered          Climacograptus         genus
    ## 4819 taxon not fully entered          Climacograptus         genus
    ## 4820 taxon not fully entered          Climacograptus         genus
    ## 4821 taxon not fully entered          Climacograptus         genus
    ## 4822 taxon not fully entered          Climacograptus         genus
    ## 4823 taxon not fully entered          Climacograptus         genus
    ## 4824 taxon not fully entered          Climacograptus         genus
    ## 4825 taxon not fully entered          Climacograptus         genus
    ## 4826 taxon not fully entered          Climacograptus         genus
    ## 4827 taxon not fully entered          Climacograptus         genus
    ## 4828 taxon not fully entered          Climacograptus         genus
    ## 4829 taxon not fully entered          Climacograptus         genus
    ## 4830 taxon not fully entered          Climacograptus         genus
    ## 4831 taxon not fully entered          Climacograptus         genus
    ## 4833                    <NA>          Climacograptus         genus
    ## 4834                    <NA>          Climacograptus         genus
    ## 4835                    <NA>          Climacograptus         genus
    ## 4836                    <NA>          Climacograptus         genus
    ## 4837                    <NA>          Climacograptus         genus
    ## 4838                    <NA>          Climacograptus         genus
    ## 4839                    <NA>          Climacograptus         genus
    ## 4883 taxon not fully entered          Climacograptus         genus
    ## 4884 taxon not fully entered          Climacograptus         genus
    ## 4885 taxon not fully entered          Climacograptus         genus
    ## 4886 taxon not fully entered          Climacograptus         genus
    ## 4887 taxon not fully entered          Climacograptus         genus
    ## 4888 taxon not fully entered          Climacograptus         genus
    ## 4889 taxon not fully entered          Climacograptus         genus
    ## 4890 taxon not fully entered          Climacograptus         genus
    ## 4891 taxon not fully entered          Climacograptus         genus
    ## 4892 taxon not fully entered          Climacograptus         genus
    ## 4893 taxon not fully entered          Climacograptus         genus
    ## 4899 taxon not fully entered          Climacograptus         genus
    ## 4900 taxon not fully entered          Climacograptus         genus
    ## 4901 taxon not fully entered          Climacograptus         genus
    ## 4902 taxon not fully entered          Climacograptus         genus
    ## 4903 taxon not fully entered          Climacograptus         genus
    ## 4904 taxon not fully entered          Climacograptus         genus
    ## 4905 taxon not fully entered          Climacograptus         genus
    ## 4906 taxon not fully entered          Climacograptus         genus
    ## 4907 taxon not fully entered          Climacograptus         genus
    ## 4908 taxon not fully entered          Climacograptus         genus
    ## 4909 taxon not fully entered          Climacograptus         genus
    ## 4910 taxon not fully entered          Climacograptus         genus
    ## 4911 taxon not fully entered          Climacograptus         genus
    ## 4912 taxon not fully entered          Climacograptus         genus
    ## 4913 taxon not fully entered          Climacograptus         genus
    ## 4914 taxon not fully entered          Climacograptus         genus
    ## 4915 taxon not fully entered          Climacograptus         genus
    ## 4916 taxon not fully entered          Climacograptus         genus
    ## 4917 taxon not fully entered          Climacograptus         genus
    ## 4918 taxon not fully entered          Climacograptus         genus
    ## 4919 taxon not fully entered          Climacograptus         genus
    ## 4920 taxon not fully entered          Climacograptus         genus
    ## 4921 taxon not fully entered          Climacograptus         genus
    ## 4923 taxon not fully entered          Climacograptus         genus
    ## 4924 taxon not fully entered          Climacograptus         genus
    ## 4925 taxon not fully entered          Climacograptus         genus
    ## 4926                    <NA>          Climacograptus         genus
    ## 4927                    <NA>          Climacograptus         genus
    ## 4928                    <NA>          Climacograptus         genus
    ## 4929                    <NA>          Climacograptus         genus
    ## 4962                    <NA> Climacograptus scalaris       species
    ## 4963                    <NA> Climacograptus scalaris       species
    ## 4964                    <NA>          Climacograptus         genus
    ## 5102 taxon not fully entered          Climacograptus         genus
    ## 5103 taxon not fully entered          Climacograptus         genus
    ## 5106 taxon not fully entered          Climacograptus         genus
    ## 5110 taxon not fully entered          Climacograptus         genus
    ## 5114 taxon not fully entered          Climacograptus         genus
    ## 5115                    <NA> Climacograptus scalaris       species
    ## 5126 taxon not fully entered          Climacograptus         genus
    ## 5127 taxon not fully entered          Climacograptus         genus
    ## 5128 taxon not fully entered          Climacograptus         genus
    ## 5129 taxon not fully entered          Climacograptus         genus
    ## 5130 taxon not fully entered          Climacograptus         genus
    ## 5131 taxon not fully entered          Climacograptus         genus
    ## 5132                    <NA> Climacograptus scalaris       species
    ## 5150 taxon not fully entered          Climacograptus         genus
    ## 5151 taxon not fully entered          Climacograptus         genus
    ## 5152 taxon not fully entered          Climacograptus         genus
    ## 5153 taxon not fully entered          Climacograptus         genus
    ## 5154                    <NA> Climacograptus scalaris       species
    ## 5155 taxon not fully entered          Climacograptus         genus
    ## 5167 taxon not fully entered          Climacograptus         genus
    ## 5176 taxon not fully entered          Climacograptus         genus
    ## 5177 taxon not fully entered          Climacograptus         genus
    ## 5195 taxon not fully entered          Climacograptus         genus
    ## 5204                    <NA> Climacograptus scalaris       species
    ## 5205 taxon not fully entered          Climacograptus         genus
    ## 5248 taxon not fully entered              Anticostia         genus
    ## 5249 taxon not fully entered              Anticostia         genus
    ## 5250 taxon not fully entered              Anticostia         genus
    ## 5251 taxon not fully entered              Anticostia         genus
    ## 5253 taxon not fully entered          Climacograptus         genus
    ## 5256 taxon not fully entered        Parareteograptus         genus
    ## 5260 taxon not fully entered            Rectograptus         genus
    ## 5261 taxon not fully entered              Anticostia         genus
    ## 5262 taxon not fully entered              Anticostia         genus
    ## 5263 taxon not fully entered              Anticostia         genus
    ## 5265 taxon not fully entered          Climacograptus         genus
    ## 5268 taxon not fully entered        Parareteograptus         genus
    ## 5270 taxon not fully entered            Rectograptus         genus
    ## 5275 taxon not fully entered              Anticostia         genus
    ## 5277 taxon not fully entered          Climacograptus         genus
    ## 5281 taxon not fully entered        Parareteograptus         genus
    ## 5286 taxon not fully entered              Anticostia         genus
    ## 5287 taxon not fully entered              Anticostia         genus
    ## 5289 taxon not fully entered          Climacograptus         genus
    ## 5293 taxon not fully entered        Parareteograptus         genus
    ## 5298 taxon not fully entered              Anticostia         genus
    ## 5299 taxon not fully entered              Anticostia         genus
    ## 5300 taxon not fully entered              Anticostia         genus
    ## 5301 taxon not fully entered              Anticostia         genus
    ## 5302 taxon not fully entered              Anticostia         genus
    ## 5305 taxon not fully entered          Climacograptus         genus
    ## 5306 taxon not fully entered          Climacograptus         genus
    ## 5307 taxon not fully entered          Climacograptus         genus
    ## 5314 taxon not fully entered        Parareteograptus         genus
    ## 5315 taxon not fully entered        Parareteograptus         genus
    ## 5319 taxon not fully entered              Anticostia         genus
    ## 5320 taxon not fully entered              Anticostia         genus
    ## 5322 taxon not fully entered            Rectograptus         genus
    ## 5323 taxon not fully entered            Rectograptus         genus
    ## 5326 taxon not fully entered              Anticostia         genus
    ## 5327 taxon not fully entered              Anticostia         genus
    ## 5330                    <NA> Climacograptus bicornis       species
    ## 5333 taxon not fully entered          Climacograptus         genus
    ## 5342                    <NA>          Climacograptus         genus
    ## 5343 taxon not fully entered          Climacograptus         genus
    ## 5344                    <NA> Climacograptus scalaris       species
    ## 5345 taxon not fully entered          Climacograptus         genus
    ## 5346 taxon not fully entered          Climacograptus         genus
    ## 5347                    <NA>          Climacograptus         genus
    ## 5353 taxon not fully entered          Climacograptus         genus
    ## 5354 taxon not fully entered          Climacograptus         genus
    ## 5355                    <NA> Climacograptus scalaris       species
    ## 5363 taxon not fully entered          Climacograptus         genus
    ## 5364 taxon not fully entered          Climacograptus         genus
    ## 5365                    <NA> Climacograptus scalaris       species
    ## 5385                    <NA> Climacograptus scalaris       species
    ## 5486 taxon not fully entered              Anticostia         genus
    ## 5487 taxon not fully entered              Anticostia         genus
    ## 5488 taxon not fully entered              Anticostia         genus
    ## 5490 taxon not fully entered          Climacograptus         genus
    ## 5495 taxon not fully entered        Parareteograptus         genus
    ## 5496 taxon not fully entered            Rectograptus         genus
    ## 5506 taxon not fully entered              Anticostia         genus
    ## 5508 taxon not fully entered          Climacograptus         genus
    ## 5513 taxon not fully entered        Parareteograptus         genus
    ## 5515 taxon not fully entered            Rectograptus         genus
    ## 5518 taxon not fully entered              Anticostia         genus
    ## 5523 taxon not fully entered        Parareteograptus         genus
    ## 5524 taxon not fully entered              Anticostia         genus
    ## 5525 taxon not fully entered          Climacograptus         genus
    ## 5530 taxon not fully entered        Parareteograptus         genus
    ## 5532 taxon not fully entered            Rectograptus         genus
    ## 5538 taxon not fully entered              Anticostia         genus
    ## 5544 taxon not fully entered        Parareteograptus         genus
    ## 5547 taxon not fully entered        Parareteograptus         genus
    ## 5548 taxon not fully entered              Anticostia         genus
    ## 5549 taxon not fully entered          Climacograptus         genus
    ## 5554 taxon not fully entered            Rectograptus         genus
    ## 5559 taxon not fully entered              Anticostia         genus
    ## 5563 taxon not fully entered        Parareteograptus         genus
    ## 5565 taxon not fully entered        Parareteograptus         genus
    ## 5567 taxon not fully entered              Anticostia         genus
    ## 5568 taxon not fully entered          Climacograptus         genus
    ## 5573 taxon not fully entered        Parareteograptus         genus
    ## 5575 taxon not fully entered            Rectograptus         genus
    ## 5585 taxon not fully entered              Anticostia         genus
    ## 5586 taxon not fully entered              Anticostia         genus
    ## 5587 taxon not fully entered              Anticostia         genus
    ## 5588 taxon not fully entered          Climacograptus         genus
    ## 5593 taxon not fully entered            Rectograptus         genus
    ## 5598 taxon not fully entered              Anticostia         genus
    ## 5599 taxon not fully entered          Climacograptus         genus
    ## 5602 taxon not fully entered            Rectograptus         genus
    ## 5606 taxon not fully entered              Anticostia         genus
    ## 5607 taxon not fully entered          Climacograptus         genus
    ## 5610 taxon not fully entered        Parareteograptus         genus
    ## 5611 taxon not fully entered            Rectograptus         genus
    ## 5613 taxon not fully entered              Anticostia         genus
    ## 5616 taxon not fully entered              Anticostia         genus
    ## 5617 taxon not fully entered              Anticostia         genus
    ## 5621 taxon not fully entered            Rectograptus         genus
    ## 5625 taxon not fully entered              Anticostia         genus
    ## 5631 taxon not fully entered              Anticostia         genus
    ## 5632 taxon not fully entered              Anticostia         genus
    ## 5633 taxon not fully entered          Climacograptus         genus
    ## 5637 taxon not fully entered            Rectograptus         genus
    ## 5641 taxon not fully entered              Anticostia         genus
    ## 5646 taxon not fully entered              Anticostia         genus
    ## 5670 taxon not fully entered            Rectograptus         genus
    ## 5673 taxon not fully entered              Anticostia         genus
    ## 5719 taxon not fully entered          Climacograptus         genus
    ## 5724 taxon not fully entered        Parareteograptus         genus
    ## 5726 taxon not fully entered            Rectograptus         genus
    ## 5727 taxon not fully entered          Climacograptus         genus
    ## 5731 taxon not fully entered            Rectograptus         genus
    ## 5732 taxon not fully entered              Anticostia         genus
    ## 5735 taxon not fully entered          Climacograptus         genus
    ## 5740 taxon not fully entered        Parareteograptus         genus
    ## 5742 taxon not fully entered            Rectograptus         genus
    ## 5743 taxon not fully entered              Anticostia         genus
    ## 5745 taxon not fully entered              Anticostia         genus
    ## 5747 taxon not fully entered        Parareteograptus         genus
    ## 5748 taxon not fully entered          Climacograptus         genus
    ## 5752 taxon not fully entered        Parareteograptus         genus
    ## 5754 taxon not fully entered            Rectograptus         genus
    ## 5760 taxon not fully entered          Climacograptus         genus
    ## 5764 taxon not fully entered        Parareteograptus         genus
    ## 5766 taxon not fully entered            Rectograptus         genus
    ## 5776 taxon not fully entered          Climacograptus         genus
    ## 5783 taxon not fully entered            Rectograptus         genus
    ## 5843 taxon not fully entered            Rectograptus         genus
    ## 5845 taxon not fully entered          Climacograptus         genus
    ## 5871                    <NA> Climacograptus scalaris       species
    ## 5886 taxon not fully entered          Climacograptus         genus
    ## 5892 taxon not fully entered          Climacograptus         genus
    ## 5896                    <NA> Climacograptus scalaris       species
    ##      accepted_no    early_interval     late_interval early_age late_age
    ## 32         33636      Whiterockian      Whiterockian     471.8    457.5
    ## 39         33636          Llanvirn          Llanvirn     466.0    460.9
    ## 56         33636        Ordovician        Ordovician     485.4    443.4
    ## 58         33636           Caradoc           Caradoc     460.9    449.5
    ## 66         33636       Black River       Black River     460.9    457.5
    ## 74         33636       Rocklandian       Rocklandian     460.9    449.5
    ## 77         33636        Ordovician        Ordovician     485.4    443.4
    ## 83         33636           Caradoc           Caradoc     460.9    449.5
    ## 89         33636         Rawtheyan         Rawtheyan     455.8    445.6
    ## 94         33636             Harju             Harju     452.0    443.7
    ## 105        33636           Caradoc           Caradoc     460.9    449.5
    ## 110        33636           Edenian           Edenian     460.9    449.5
    ## 115        33636           Edenian           Edenian     460.9    449.5
    ## 117        33636           Edenian           Edenian     460.9    449.5
    ## 120        33636           Edenian           Edenian     460.9    449.5
    ## 122        33636       Maysvillian       Maysvillian     452.0    449.5
    ## 128        33636        Llandovery        Llandovery     443.4    433.4
    ## 131        33636        Llandovery        Llandovery     443.4    433.4
    ## 152        33636           Pridoli           Pridoli     423.0    419.2
    ## 156        33636        Llandovery        Llandovery     443.4    433.4
    ## 181        33636           Ashgill           Ashgill     449.5    443.7
    ## 192        33636           Caradoc           Caradoc     460.9    449.5
    ## 194        33636        Shermanian        Shermanian     460.9    449.5
    ## 214        33636         Eastonian         Eastonian     456.1    449.5
    ## 226        33636         Eastonian            Onnian     456.1    449.5
    ## 233       316364          Aeronian          Aeronian     440.8    438.5
    ## 234        33636          Aeronian          Aeronian     440.8    438.5
    ## 236       316364          Aeronian          Aeronian     440.8    438.5
    ## 237        33636          Aeronian          Aeronian     440.8    438.5
    ## 257        33636         Soudleyan     Marshbrookian     457.5    452.0
    ## 259        33636         Costonian         Harnagian     460.9    455.8
    ## 261        33636         Costonian         Harnagian     460.9    455.8
    ## 264        33636           Idavere           Idavere     460.9    455.8
    ## 267        33636          Actonian            Onnian     455.8    449.5
    ## 269        33636          Actonian            Onnian     455.8    449.5
    ## 273        33636        Pusgillian        Pusgillian     449.5    445.6
    ## 276        33636     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 283        33636     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 294        33636         Soudleyan     Marshbrookian     457.5    452.0
    ## 298        33636        Pusgillian        Pusgillian     449.5    445.6
    ## 303        33636   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 312        33636     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 400        33636             Sarka             Sarka     466.0    466.0
    ## 411        33636   Late Ordovician            Vinice     458.4    455.8
    ## 415       270339   Late Ordovician            Vinice     458.4    455.8
    ## 416        33636   Late Ordovician          Zahorany     458.4    455.8
    ## 418       270339   Late Ordovician          Zahorany     458.4    455.8
    ## 422       270339       Longvillian            Onnian     457.5    449.5
    ## 436        33636 Middle Ordovician Middle Ordovician     470.0    458.4
    ## 444        33636   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 472        33636            Arenig            Arenig     478.6    466.0
    ## 482        33636    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 489        33636           Caradoc           Caradoc     460.9    449.5
    ## 493        33636           Caradoc           Caradoc     460.9    449.5
    ## 502        33636           Ashgill           Ashgill     449.5    443.7
    ## 511        33636            Arenig            Arenig     478.6    466.0
    ## 523        33636         Llandeilo         Llandeilo     466.0    449.5
    ## 529        33636          Llanvirn          Llanvirn     466.0    460.9
    ## 534        33636            Arenig            Arenig     478.6    466.0
    ## 544        33636         Llandeilo         Llandeilo     466.0    449.5
    ## 549        33636          Llanvirn          Llanvirn     466.0    460.9
    ## 553        33636         Costonian     Marshbrookian     460.9    452.0
    ## 560        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 571        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 579        33636         Costonian         Harnagian     460.9    455.8
    ## 586        33636  Middle Llandeilo    Late Llandeilo     460.9    449.5
    ## 587        33636   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 627        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 634        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 641        33636            Wufeng            Wufeng     449.5    443.7
    ## 659        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 665        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 666        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 670        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 698        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 706        33636            Arenig            Arenig     478.6    466.0
    ## 725        33636    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 729        33636         Rawtheyan         Cautleyan     455.8    445.6
    ## 734        33636         Rawtheyan        Pusgillian     455.8    445.6
    ## 738        33636         Rawtheyan         Cautleyan     455.8    445.6
    ## 741        33636         Rawtheyan         Cautleyan     455.8    445.6
    ## 746        33636          Actonian            Onnian     455.8    449.5
    ## 759        33636          Actonian            Onnian     455.8    449.5
    ## 791        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 795        33636            Wufeng            Wufeng     449.5    443.7
    ## 808        33636            Wufeng            Wufeng     449.5    443.7
    ## 813        33636          Actonian            Onnian     455.8    449.5
    ## 819        33636            Wufeng        Hirnantian     449.5    443.4
    ## 837        33636         Rawtheyan            Wufeng     455.8    443.7
    ## 865        33636    Late Llandeilo    Late Llandeilo     460.9    449.5
    ## 887        33636            Wufeng        Hirnantian     449.5    443.4
    ## 891        33636          Llanvirn          Llanvirn     466.0    460.9
    ## 918        33636            Wufeng            Wufeng     449.5    443.7
    ## 920        33636            Wufeng            Wufeng     449.5    443.7
    ## 923        33636          Actonian            Onnian     455.8    449.5
    ## 929        33636         Costonian         Harnagian     460.9    455.8
    ## 933        33636         Llandeilo         Llandeilo     466.0    449.5
    ## 949        33636            Wufeng        Hirnantian     449.5    443.4
    ## 960        33636            Wufeng        Hirnantian     449.5    443.4
    ## 968        33636         Llandeilo         Llandeilo     466.0    449.5
    ## 1000       33636            Wufeng        Hirnantian     449.5    443.4
    ## 1003       33636         Rawtheyan            Wufeng     455.8    443.7
    ## 1012       33636         Costonian         Harnagian     460.9    455.8
    ## 1016       33636              Hulo              Hulo     468.1    460.9
    ## 1027       33636           Ningkuo           Ningkuo     478.6    468.1
    ## 1059       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 1086       33636           Ashgill           Ashgill     449.5    443.7
    ## 1090       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 1101       33636           Ningkuo           Ningkuo     478.6    468.1
    ## 1130       33636        Hirnantian        Hirnantian     445.2    443.4
    ## 1138       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 1163       33636        Hirnantian        Hirnantian     445.2    443.4
    ## 1166       33636           Ashgill           Ashgill     449.5    443.7
    ## 1213       33636        Pusgillian        Pusgillian     449.5    445.6
    ## 1215       33636           Ningkuo           Ningkuo     478.6    468.1
    ## 1221       33636           Ningkuo           Ningkuo     478.6    468.1
    ## 1229       33636           Ningkuo           Ningkuo     478.6    468.1
    ## 1247       33636            Wufeng            Wufeng     449.5    443.7
    ## 1252       33636         Rawtheyan            Wufeng     455.8    443.7
    ## 1273       33636         Rawtheyan            Wufeng     455.8    443.7
    ## 1285       33636         Rawtheyan            Wufeng     455.8    443.7
    ## 1290       33636         Rawtheyan            Wufeng     455.8    443.7
    ## 1305       33636            Wufeng           Ashgill     449.5    443.7
    ## 1309       33636           Ashgill           Ashgill     449.5    443.7
    ## 1315      150197         Rawtheyan         Rawtheyan     455.8    445.6
    ## 1316       33636         Rawtheyan         Rawtheyan     455.8    445.6
    ## 1317       33636         Rawtheyan         Rawtheyan     455.8    445.6
    ## 1360       33636         Costonian       Longvillian     460.9    455.8
    ## 1394       33636         Costonian         Costonian     460.9    457.5
    ## 1412       33636          Actonian            Onnian     455.8    449.5
    ## 1416       33636          Actonian            Onnian     455.8    449.5
    ## 1432       33636         Costonian         Harnagian     460.9    455.8
    ## 1465       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 1473       33636           Caradoc           Caradoc     460.9    449.5
    ## 1554       33636           Ashgill           Ashgill     449.5    443.7
    ## 1556       33636           Ashgill           Ashgill     449.5    443.7
    ## 1566       33636           Ashgill           Ashgill     449.5    443.7
    ## 1568       33636           Ashgill           Ashgill     449.5    443.7
    ## 1569       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 1571       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 1573       33636        Caradocian        Caradocian     460.9    449.5
    ## 1574       33636        Caradocian        Caradocian     460.9    449.5
    ## 1575       33636        Caradocian        Caradocian     460.9    449.5
    ## 1579       33636           Ashgill           Ashgill     449.5    443.7
    ## 1580       33636           Ashgill           Ashgill     449.5    443.7
    ## 1581       33636           Ashgill           Ashgill     449.5    443.7
    ## 1582       33636           Ashgill           Ashgill     449.5    443.7
    ## 1586       33636           Ashgill           Ashgill     449.5    443.7
    ## 1590       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1591       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1596       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1597       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1599       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1600       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1601       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1605       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1606       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1612       33636        Rhuddanian          Aeronian     443.4    438.5
    ## 1613      316364        Rhuddanian          Aeronian     443.4    438.5
    ## 1637      316364          Aeronian          Aeronian     440.8    438.5
    ## 1648      316364          Aeronian          Aeronian     440.8    438.5
    ## 1839       33636        Llandovery        Llandovery     443.4    433.4
    ## 2120       33636         Soudleyan     Marshbrookian     457.5    452.0
    ## 2124       33636         Costonian         Harnagian     460.9    455.8
    ## 2128       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 2140       33636         Harnagian     Marshbrookian     457.5    452.0
    ## 2150       33636         Costonian         Harnagian     460.9    455.8
    ## 2166       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 2173       33636         Costonian         Harnagian     460.9    455.8
    ## 2185       33636         Cautleyan        Hirnantian     449.5    443.4
    ## 2192       33636        Pusgillian        Pusgillian     449.5    445.6
    ## 2199       33636         Soudleyan     Marshbrookian     457.5    452.0
    ## 2202       33636          Llanvirn          Llanvirn     466.0    460.9
    ## 2211       33636           Ashgill           Ashgill     449.5    443.7
    ## 2214       33636           Caradoc           Caradoc     460.9    449.5
    ## 2224       33636          Llanvirn          Llanvirn     466.0    460.9
    ## 2234       33636         Cautleyan        Hirnantian     449.5    443.4
    ## 2239       33636         Soudleyan            Onnian     457.5    449.5
    ## 2246       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 2256       33636            Arenig            Arenig     478.6    466.0
    ## 2291       33636          Llanvirn         Llandeilo     466.0    449.5
    ## 2317       33636           Caradoc           Caradoc     460.9    449.5
    ## 2325       33636           Caradoc           Caradoc     460.9    449.5
    ## 2328       33636           Caradoc           Caradoc     460.9    449.5
    ## 2341       33636    Late Llandeilo    Late Llandeilo     460.9    449.5
    ## 2347       33636          Llanvirn          Llanvirn     466.0    460.9
    ## 2362       33636         Llandeilo           Caradoc     466.0    449.5
    ## 2368       33636           Ashgill           Ashgill     449.5    443.7
    ## 2376       33636           Ashgill           Ashgill     449.5    443.7
    ## 2379       33636           Caradoc           Caradoc     460.9    449.5
    ## 2399      306375        Trentonian       Richmondian     460.9    443.7
    ## 2400       33636        Trentonian       Richmondian     460.9    443.7
    ## 2413       33636           Ashgill        Llandovery     449.5    433.4
    ## 2424       33636   Late Ordovician   Late Ordovician     458.4    443.4
    ## 2425       33636   Late Ordovician   Late Ordovician     458.4    443.4
    ## 2437      316364       Alexandrian          Ontarian     443.4    428.2
    ## 2456       33636           Ashgill           Ashgill     449.5    443.7
    ## 2459       33636       Alexandrian       Alexandrian     443.4    436.0
    ## 2463       33636       Alexandrian       Alexandrian     443.4    436.0
    ## 2464       33636       Alexandrian       Alexandrian     443.4    436.0
    ## 2466       33636       Alexandrian       Alexandrian     443.4    436.0
    ## 2501       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 2502       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 2505       33636           Wenlock           Wenlock     433.4    427.4
    ## 2507       33636 Middle Ordovician Middle Ordovician     470.0    458.4
    ## 2508       33636 Middle Ordovician Middle Ordovician     470.0    458.4
    ## 2518       33636   Late Ordovician          Silurian     458.4    419.2
    ## 2520       33636           Ashgill        Llandovery     449.5    433.4
    ## 2521       33636           Ashgill        Llandovery     449.5    433.4
    ## 2525       33636       Richmondian         Gamachian     449.5    443.7
    ## 2526       33636       Richmondian         Gamachian     449.5    443.7
    ## 2527       33636       Richmondian         Gamachian     449.5    443.7
    ## 2528       33636       Richmondian         Gamachian     449.5    443.7
    ## 2530      316364       Alexandrian       Alexandrian     443.4    436.0
    ## 2562      306375        Caradocian        Caradocian     460.9    449.5
    ## 2565      306375        Shermanian       Maysvillian     460.9    449.5
    ## 2585       33636        Caradocian           Ashgill     460.9    443.7
    ## 2587       33636        Caradocian        Caradocian     460.9    449.5
    ## 2593       33636        Caradocian        Caradocian     460.9    449.5
    ## 2644       33636       Dobrotivian         Berounian     460.9    449.5
    ## 2646       33636       Dobrotivian       Dobrotivian     460.9    457.5
    ## 2661       33636       Dobrotivian         Berounian     460.9    449.5
    ## 2706      150197         Telychian      Sheinwoodian     438.5    430.5
    ## 2707       33636         Telychian      Sheinwoodian     438.5    430.5
    ## 2708       33636        Llandovery        Llandovery     443.4    433.4
    ## 2710       33636        Llandovery        Llandovery     443.4    433.4
    ## 2755       33636           Pridoli           Pridoli     423.0    419.2
    ## 2793       33636        Caradocian        Caradocian     460.9    449.5
    ## 2797       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 2798       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 2799       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 2804       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 2806       33636        Caradocian        Caradocian     460.9    449.5
    ## 2807       33636        Caradocian        Caradocian     460.9    449.5
    ## 2809       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 2810       33636       Maysvillian       Maysvillian     452.0    449.5
    ## 2884      316364        Llandovery        Llandovery     443.4    433.4
    ## 2891       33636          Aeronian         Telychian     440.8    433.4
    ## 2892       33636          Aeronian         Telychian     440.8    433.4
    ## 2893       33636          Aeronian         Telychian     440.8    433.4
    ## 2934      316364          Aeronian          Aeronian     440.8    438.5
    ## 2935       33636          Aeronian          Aeronian     440.8    438.5
    ## 2943       33636        Rhuddanian          Aeronian     443.4    438.5
    ## 2948      316364        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3021      316364          Aeronian         Telychian     440.8    433.4
    ## 3108       33636        Llandovery        Llandovery     443.4    433.4
    ## 3110       33636        Llandovery        Llandovery     443.4    433.4
    ## 3116       33636        Llandovery        Llandovery     443.4    433.4
    ## 3127       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3128       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3129       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3148       33636        Llandovery        Llandovery     443.4    433.4
    ## 3149       33636        Llandovery        Llandovery     443.4    433.4
    ## 3173      316364        Llandovery        Llandovery     443.4    433.4
    ## 3182       33636        Llandovery        Llandovery     443.4    433.4
    ## 3199       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3200       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3202       33636         Telychian         Telychian     438.5    433.4
    ## 3246      316364        Llandovery        Llandovery     443.4    433.4
    ## 3248       33636        Llandovery        Llandovery     443.4    433.4
    ## 3276       33636          Aeronian          Aeronian     440.8    438.5
    ## 3290       33636        Llandovery        Llandovery     443.4    433.4
    ## 3318       33636        Llandovery        Llandovery     443.4    433.4
    ## 3353       33636        Llandovery        Llandovery     443.4    433.4
    ## 3358       33636        Llandovery        Llandovery     443.4    433.4
    ## 3366       33636         Rawtheyan        Hirnantian     455.8    443.4
    ## 3377       33636           Ashgill           Ashgill     449.5    443.7
    ## 3386       33636        Llandovery        Llandovery     443.4    433.4
    ## 3403       33636           Edenian           Edenian     460.9    449.5
    ## 3462       33636        Pusgillian        Pusgillian     449.5    445.6
    ## 3473       33636         Llandeilo         Llandeilo     466.0    449.5
    ## 3479       33636          Llanvirn          Llanvirn     466.0    460.9
    ## 3485       33636    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 3530       33636 Middle Ordovician   Late Ordovician     470.0    443.4
    ## 3541       33636           Ashgill           Ashgill     449.5    443.7
    ## 3545       33636           Caradoc           Caradoc     460.9    449.5
    ## 3677       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3842       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 3847      150197        Gisbornian        Gisbornian     460.9    456.1
    ## 3848      150197        Gisbornian        Gisbornian     460.9    456.1
    ## 3849      150197        Gisbornian        Gisbornian     460.9    456.1
    ## 3857      150197        Gisbornian        Gisbornian     460.9    456.1
    ## 3859       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3866       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3867       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3894       33636       Darriwilian        Gisbornian     467.3    456.1
    ## 3903       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 3912       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3919       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 3937      150197       Darriwilian       Darriwilian     467.3    458.4
    ## 3941       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3942       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3949       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3956       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 3968       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 3979       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3983       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 3998       33636       Darriwilian       Darriwilian     467.3    458.4
    ## 4011       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4023       33636         Bolindian         Bolindian     449.5    443.7
    ## 4038       33636        Llandovery        Llandovery     443.4    433.4
    ## 4041       33636            Wufeng            Wufeng     449.5    443.7
    ## 4046       33636            Wufeng            Wufeng     449.5    443.7
    ## 4051      270338            Wufeng            Wufeng     449.5    443.7
    ## 4061       33636           Caradoc           Caradoc     460.9    449.5
    ## 4062       33636           Caradoc           Caradoc     460.9    449.5
    ## 4067       33636           Caradoc           Caradoc     460.9    449.5
    ## 4072       33636           Caradoc           Caradoc     460.9    449.5
    ## 4075       33636           Caradoc           Caradoc     460.9    449.5
    ## 4096       33636        Shermanian        Shermanian     460.9    449.5
    ## 4097       33636        Shermanian        Shermanian     460.9    449.5
    ## 4099       33636        Shermanian        Shermanian     460.9    449.5
    ## 4101       33636        Shermanian        Shermanian     460.9    449.5
    ## 4102       33636        Shermanian        Shermanian     460.9    449.5
    ## 4104       33636           Caradoc           Caradoc     460.9    449.5
    ## 4110       33636           Caradoc           Caradoc     460.9    449.5
    ## 4113       33636           Caradoc           Caradoc     460.9    449.5
    ## 4115       33636           Caradoc           Caradoc     460.9    449.5
    ## 4138       33636           Caradoc           Caradoc     460.9    449.5
    ## 4141       33636           Caradoc           Caradoc     460.9    449.5
    ## 4142       33636           Caradoc           Caradoc     460.9    449.5
    ## 4150       33636       Richmondian       Richmondian     449.5    443.7
    ## 4166      306375           Idavere           Idavere     460.9    455.8
    ## 4167       33636           Idavere           Idavere     460.9    455.8
    ## 4256       33636      Whiterockian      Whiterockian     471.8    457.5
    ## 4257       33636      Whiterockian      Whiterockian     471.8    457.5
    ## 4266       33636      Whiterockian      Whiterockian     471.8    457.5
    ## 4267       33636      Whiterockian      Whiterockian     471.8    457.5
    ## 4286       33636      Whiterockian      Whiterockian     471.8    457.5
    ## 4292       33636         Mohawkian         Mohawkian     457.5    452.5
    ## 4293       33636         Mohawkian         Mohawkian     457.5    452.5
    ## 4302       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4303       33636 Middle Ordovician   Late Ordovician     470.0    443.4
    ## 4305       33636 Middle Ordovician   Late Ordovician     470.0    443.4
    ## 4309       33636         Arenigian           Chazyan     478.6    460.9
    ## 4316       33636        Ordovician        Ordovician     485.4    443.4
    ## 4317       33636        Ordovician        Ordovician     485.4    443.4
    ## 4320      306375   Late Ordovician   Late Ordovician     458.4    443.4
    ## 4325      306375   Late Ordovician   Late Ordovician     458.4    443.4
    ## 4332      306375   Late Ordovician   Late Ordovician     458.4    443.4
    ## 4333       33636   Late Ordovician   Late Ordovician     458.4    443.4
    ## 4340       33636          Silurian          Silurian     443.4    419.2
    ## 4345       33636        Caradocian        Caradocian     460.9    449.5
    ## 4350       33636        Caradocian        Caradocian     460.9    449.5
    ## 4353       33636        Ashgillian        Llandovery     449.5    433.4
    ## 4354      316364        Ashgillian        Llandovery     449.5    433.4
    ## 4355       33636        Ashgillian        Llandovery     449.5    433.4
    ## 4358       33636        Caradocian        Caradocian     460.9    449.5
    ## 4366       33636        Caradocian        Caradocian     460.9    449.5
    ## 4379       33636        Caradocian        Caradocian     460.9    449.5
    ## 4386       33636        Caradocian        Caradocian     460.9    449.5
    ## 4391       33636        Caradocian        Caradocian     460.9    449.5
    ## 4402       33636        Caradocian        Caradocian     460.9    449.5
    ## 4413       33636        Caradocian        Caradocian     460.9    449.5
    ## 4414       33636        Caradocian        Caradocian     460.9    449.5
    ## 4436       33636        Caradocian        Caradocian     460.9    449.5
    ## 4444       33636       Llanvirnian       Llanvirnian     468.1    460.9
    ## 4498       33636        Caradocian        Ashgillian     460.9    443.7
    ## 4501       33636        Caradocian        Llandovery     460.9    433.4
    ## 4516      306375          Sandbian          Sandbian     458.4    453.0
    ## 4522       33636          Sandbian          Sandbian     458.4    453.0
    ## 4662       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4667       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4671       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4673       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4685      306375        Gisbornian        Gisbornian     460.9    456.1
    ## 4686       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4695      306375        Gisbornian        Gisbornian     460.9    456.1
    ## 4703      306375        Gisbornian        Gisbornian     460.9    456.1
    ## 4713      306375        Gisbornian        Gisbornian     460.9    456.1
    ## 4725      306375        Gisbornian        Gisbornian     460.9    456.1
    ## 4726       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4748       33636       Llandeilian       Llandeilian     466.0    460.9
    ## 4756       33636       Llandeilian       Llandeilian     466.0    460.9
    ## 4765       33636        Gisbornian        Gisbornian     460.9    456.1
    ## 4773      306375         Eastonian         Eastonian     456.1    449.5
    ## 4774      306375         Eastonian         Eastonian     456.1    449.5
    ## 4775      306375         Eastonian         Eastonian     456.1    449.5
    ## 4776       33636         Eastonian         Eastonian     456.1    449.5
    ## 4777       33636         Eastonian         Eastonian     456.1    449.5
    ## 4780       33636         Eastonian         Eastonian     456.1    449.5
    ## 4781       33636         Eastonian         Eastonian     456.1    449.5
    ## 4782       33636         Eastonian         Eastonian     456.1    449.5
    ## 4816       33636         Eastonian         Eastonian     456.1    449.5
    ## 4817       33636         Eastonian         Eastonian     456.1    449.5
    ## 4818       33636         Eastonian         Eastonian     456.1    449.5
    ## 4819       33636         Eastonian         Eastonian     456.1    449.5
    ## 4820       33636         Eastonian         Eastonian     456.1    449.5
    ## 4821       33636         Eastonian         Eastonian     456.1    449.5
    ## 4822       33636         Eastonian         Eastonian     456.1    449.5
    ## 4823       33636         Eastonian         Eastonian     456.1    449.5
    ## 4824       33636         Eastonian         Eastonian     456.1    449.5
    ## 4825       33636         Eastonian         Eastonian     456.1    449.5
    ## 4826       33636         Eastonian         Eastonian     456.1    449.5
    ## 4827       33636         Eastonian         Eastonian     456.1    449.5
    ## 4828       33636         Eastonian         Eastonian     456.1    449.5
    ## 4829       33636         Eastonian         Eastonian     456.1    449.5
    ## 4830       33636         Eastonian         Eastonian     456.1    449.5
    ## 4831       33636         Eastonian         Eastonian     456.1    449.5
    ## 4833       33636         Eastonian         Eastonian     456.1    449.5
    ## 4834       33636         Eastonian         Eastonian     456.1    449.5
    ## 4835       33636         Eastonian         Eastonian     456.1    449.5
    ## 4836       33636         Eastonian         Eastonian     456.1    449.5
    ## 4837       33636         Eastonian         Eastonian     456.1    449.5
    ## 4838       33636         Eastonian         Eastonian     456.1    449.5
    ## 4839       33636         Eastonian         Eastonian     456.1    449.5
    ## 4883       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4884       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4885       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4886       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4887       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4888       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4889       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4890       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4891       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4892       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4893       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4899       33636         Bolindian         Bolindian     449.5    443.7
    ## 4900       33636         Bolindian         Bolindian     449.5    443.7
    ## 4901       33636         Bolindian         Bolindian     449.5    443.7
    ## 4902       33636         Bolindian         Bolindian     449.5    443.7
    ## 4903       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4904       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4905       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4906       33636         Bolindian         Bolindian     449.5    443.7
    ## 4907       33636         Bolindian         Bolindian     449.5    443.7
    ## 4908       33636         Bolindian         Bolindian     449.5    443.7
    ## 4909       33636         Bolindian         Bolindian     449.5    443.7
    ## 4910       33636         Bolindian         Bolindian     449.5    443.7
    ## 4911       33636         Bolindian         Bolindian     449.5    443.7
    ## 4912       33636         Bolindian         Bolindian     449.5    443.7
    ## 4913       33636         Bolindian         Bolindian     449.5    443.7
    ## 4914       33636         Bolindian         Bolindian     449.5    443.7
    ## 4915       33636         Bolindian         Bolindian     449.5    443.7
    ## 4916       33636         Bolindian         Bolindian     449.5    443.7
    ## 4917       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4918       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4919       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4920       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4921       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4923       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4924       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4925       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4926       33636         Bolindian         Bolindian     449.5    443.7
    ## 4927       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4928       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4929       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 4962      316364          Aeronian          Aeronian     440.8    438.5
    ## 4963      316364          Aeronian          Aeronian     440.8    438.5
    ## 4964       33636          Aeronian          Aeronian     440.8    438.5
    ## 5102       33636        Llandovery        Llandovery     443.4    433.4
    ## 5103       33636        Llandovery        Llandovery     443.4    433.4
    ## 5106       33636        Llandovery        Llandovery     443.4    433.4
    ## 5110       33636        Llandovery        Llandovery     443.4    433.4
    ## 5114       33636        Llandovery        Llandovery     443.4    433.4
    ## 5115      316364        Llandovery        Llandovery     443.4    433.4
    ## 5126       33636        Llandovery        Llandovery     443.4    433.4
    ## 5127       33636        Llandovery        Llandovery     443.4    433.4
    ## 5128       33636        Llandovery        Llandovery     443.4    433.4
    ## 5129       33636        Llandovery        Llandovery     443.4    433.4
    ## 5130       33636        Llandovery        Llandovery     443.4    433.4
    ## 5131       33636        Llandovery        Llandovery     443.4    433.4
    ## 5132      316364        Llandovery        Llandovery     443.4    433.4
    ## 5150       33636        Llandovery        Llandovery     443.4    433.4
    ## 5151       33636        Llandovery        Llandovery     443.4    433.4
    ## 5152       33636        Llandovery        Llandovery     443.4    433.4
    ## 5153       33636        Llandovery        Llandovery     443.4    433.4
    ## 5154      316364        Llandovery        Llandovery     443.4    433.4
    ## 5155       33636        Llandovery        Llandovery     443.4    433.4
    ## 5167       33636        Llandovery        Llandovery     443.4    433.4
    ## 5176       33636        Llandovery        Llandovery     443.4    433.4
    ## 5177       33636        Llandovery        Llandovery     443.4    433.4
    ## 5195       33636        Llandovery        Llandovery     443.4    433.4
    ## 5204      316364        Llandovery        Llandovery     443.4    433.4
    ## 5205       33636        Llandovery        Llandovery     443.4    433.4
    ## 5248      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5249      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5250      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5251      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5253       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5256      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5260      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5261      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5262      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5263      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5265       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5268      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5270      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5275      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5277       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5281      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5286      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5287      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5289       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5293      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5298      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5299      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5300      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5301      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5302      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5305       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5306       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5307       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5314      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5315      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5319      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5320      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5322      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5323      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5326      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5327      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5330      306375        Caradocian        Caradocian     460.9    449.5
    ## 5333       33636        Caradocian        Caradocian     460.9    449.5
    ## 5342       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5343       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5344      316364        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5345       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5346       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5347       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5353       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5354       33636        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5355      316364        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5363       33636          Aeronian          Aeronian     440.8    438.5
    ## 5364       33636          Aeronian          Aeronian     440.8    438.5
    ## 5365      316364          Aeronian          Aeronian     440.8    438.5
    ## 5385      316364          Aeronian          Aeronian     440.8    438.5
    ## 5486      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5487      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5488      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5490       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5495      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5496      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5506      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5508       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5513      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5515      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5518      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5523      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5524      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5525       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5530      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5532      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5538      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5544      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5547      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5548      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5549       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5554      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5559      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5563      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5565      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5567      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5568       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5573      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5575      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5585      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5586      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5587      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5588       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5593      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5598      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5599       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5602      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5606      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5607       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5610      270338        Ashgillian        Ashgillian     449.5    443.7
    ## 5611      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5613      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5616      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5617      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5621      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5625      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5631      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5632      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5633       33636        Ashgillian        Ashgillian     449.5    443.7
    ## 5637      270339        Ashgillian        Ashgillian     449.5    443.7
    ## 5641      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5646      270341        Ashgillian        Ashgillian     449.5    443.7
    ## 5670      270339        Hirnantian        Hirnantian     445.2    443.4
    ## 5673      270341        Hirnantian        Hirnantian     445.2    443.4
    ## 5719       33636            Katian            Katian     453.0    445.2
    ## 5724      270338            Katian            Katian     453.0    445.2
    ## 5726      270339            Katian            Katian     453.0    445.2
    ## 5727       33636            Katian            Katian     453.0    445.2
    ## 5731      270339            Katian            Katian     453.0    445.2
    ## 5732      270341            Katian            Katian     453.0    445.2
    ## 5735       33636            Katian            Katian     453.0    445.2
    ## 5740      270338            Katian            Katian     453.0    445.2
    ## 5742      270339            Katian            Katian     453.0    445.2
    ## 5743      270341            Katian            Katian     453.0    445.2
    ## 5745      270341            Katian            Katian     453.0    445.2
    ## 5747      270338            Katian            Katian     453.0    445.2
    ## 5748       33636            Katian            Katian     453.0    445.2
    ## 5752      270338            Katian            Katian     453.0    445.2
    ## 5754      270339            Katian            Katian     453.0    445.2
    ## 5760       33636            Katian            Katian     453.0    445.2
    ## 5764      270338            Katian            Katian     453.0    445.2
    ## 5766      270339            Katian            Katian     453.0    445.2
    ## 5776       33636            Katian            Katian     453.0    445.2
    ## 5783      270339            Katian            Katian     453.0    445.2
    ## 5843      270339            Katian            Katian     453.0    445.2
    ## 5845       33636        Hirnantian        Hirnantian     445.2    443.4
    ## 5871      316364          Aeronian          Aeronian     440.8    438.5
    ## 5886       33636        Pusgillian        Pusgillian     449.5    445.6
    ## 5892       33636       Longvillian     Marshbrookian     457.5    452.0
    ## 5896      316364         Bolindian         Bolindian     449.5    443.7
    ##      reference_no     primary_name primary_reso subgenus_name
    ## 32             13   Climacograptus         <NA>          <NA>
    ## 39             13   Climacograptus         <NA>          <NA>
    ## 56             13   Climacograptus         <NA>          <NA>
    ## 58             13   Climacograptus         <NA>          <NA>
    ## 66             13   Climacograptus         <NA>          <NA>
    ## 74             13   Climacograptus         <NA>          <NA>
    ## 77             13   Climacograptus         <NA>          <NA>
    ## 83          17050   Climacograptus         <NA>          <NA>
    ## 89             13   Climacograptus         <NA>          <NA>
    ## 94             13   Climacograptus         <NA>          <NA>
    ## 105            13   Climacograptus         <NA>          <NA>
    ## 110            13   Climacograptus         <NA>          <NA>
    ## 115            13   Climacograptus         <NA>          <NA>
    ## 117            13   Climacograptus         <NA>          <NA>
    ## 120            13   Climacograptus         <NA>          <NA>
    ## 122            13   Climacograptus         <NA>          <NA>
    ## 128            13   Climacograptus         <NA>          <NA>
    ## 131            13   Climacograptus         <NA>          <NA>
    ## 152            13   Climacograptus         <NA>          <NA>
    ## 156            13   Climacograptus         <NA>          <NA>
    ## 181            13   Climacograptus         <NA>          <NA>
    ## 192            13   Climacograptus         <NA>          <NA>
    ## 194            13   Climacograptus         <NA>          <NA>
    ## 214            78   Climacograptus         <NA>          <NA>
    ## 226            87   Climacograptus         <NA>          <NA>
    ## 233           155   Climacograptus         <NA>          <NA>
    ## 234           155   Climacograptus         <NA>          <NA>
    ## 236           155   Climacograptus         <NA>          <NA>
    ## 237           155   Climacograptus         <NA>          <NA>
    ## 257           102   Climacograptus         <NA>          <NA>
    ## 259           103   Climacograptus         <NA>          <NA>
    ## 261           103   Climacograptus         <NA>          <NA>
    ## 264           103   Climacograptus         <NA>          <NA>
    ## 267           103   Climacograptus         <NA>          <NA>
    ## 269           103   Climacograptus         <NA>          <NA>
    ## 273           103   Climacograptus         <NA>          <NA>
    ## 276           104   Climacograptus         <NA>          <NA>
    ## 283           104   Climacograptus         <NA>          <NA>
    ## 294           108   Climacograptus         <NA>          <NA>
    ## 298           107   Climacograptus         <NA>          <NA>
    ## 303           107   Climacograptus         <NA>          <NA>
    ## 312           116   Climacograptus         <NA>          <NA>
    ## 400           227   Climacograptus         <NA>          <NA>
    ## 411           227   Climacograptus         <NA>          <NA>
    ## 415           227     Rectograptus         <NA>          <NA>
    ## 416           227   Climacograptus         <NA>          <NA>
    ## 418           227     Rectograptus         <NA>          <NA>
    ## 422           227     Rectograptus         <NA>          <NA>
    ## 436           437   Climacograptus         <NA>          <NA>
    ## 444           107   Climacograptus         <NA>          <NA>
    ## 472           285   Climacograptus         <NA>          <NA>
    ## 482           285   Climacograptus         <NA>          <NA>
    ## 489           285   Climacograptus         <NA>          <NA>
    ## 493           285   Climacograptus         <NA>          <NA>
    ## 502           285   Climacograptus         <NA>          <NA>
    ## 511           286   Climacograptus         <NA>          <NA>
    ## 523           286   Climacograptus         <NA>          <NA>
    ## 529           286   Climacograptus         <NA>          <NA>
    ## 534           286   Climacograptus         <NA>          <NA>
    ## 544           286   Climacograptus         <NA>          <NA>
    ## 549           286   Climacograptus         <NA>          <NA>
    ## 553           286   Climacograptus         <NA>          <NA>
    ## 560           287   Climacograptus         <NA>          <NA>
    ## 571           287   Climacograptus         <NA>          <NA>
    ## 579           287   Climacograptus         <NA>          <NA>
    ## 586           287   Climacograptus         <NA>          <NA>
    ## 587           287   Climacograptus         <NA>          <NA>
    ## 627           288   Climacograptus         <NA>          <NA>
    ## 634           288   Climacograptus         <NA>          <NA>
    ## 641           288   Climacograptus         <NA>          <NA>
    ## 659           288   Climacograptus         <NA>          <NA>
    ## 665           288   Climacograptus         <NA>          <NA>
    ## 666           288   Climacograptus         <NA>          <NA>
    ## 670           288   Climacograptus         <NA>          <NA>
    ## 698           288   Climacograptus         <NA>          <NA>
    ## 706           288   Climacograptus         <NA>          <NA>
    ## 725           288   Climacograptus         <NA>          <NA>
    ## 729           288   Climacograptus         <NA>          <NA>
    ## 734           288   Climacograptus         <NA>          <NA>
    ## 738           288   Climacograptus         <NA>          <NA>
    ## 741           288   Climacograptus         <NA>          <NA>
    ## 746           288   Climacograptus         <NA>          <NA>
    ## 759           288   Climacograptus         <NA>          <NA>
    ## 791           475   Climacograptus         <NA>          <NA>
    ## 795           475   Climacograptus         <NA>          <NA>
    ## 808           475   Climacograptus         <NA>          <NA>
    ## 813           475   Climacograptus         <NA>          <NA>
    ## 819           485   Climacograptus         <NA>          <NA>
    ## 837           485   Climacograptus         <NA>          <NA>
    ## 865           485   Climacograptus         <NA>          <NA>
    ## 887           476   Climacograptus         <NA>          <NA>
    ## 891           476   Climacograptus         <NA>          <NA>
    ## 918           476   Climacograptus         <NA>          <NA>
    ## 920           476   Climacograptus         <NA>          <NA>
    ## 923           476   Climacograptus         <NA>          <NA>
    ## 929           476   Climacograptus         <NA>          <NA>
    ## 933           476   Climacograptus         <NA>          <NA>
    ## 949           477   Climacograptus         <NA>          <NA>
    ## 960           477   Climacograptus         <NA>          <NA>
    ## 968           477   Climacograptus         <NA>          <NA>
    ## 1000          479   Climacograptus         <NA>          <NA>
    ## 1003          479   Climacograptus         <NA>          <NA>
    ## 1012          479   Climacograptus         <NA>          <NA>
    ## 1016          479   Climacograptus         <NA>          <NA>
    ## 1027          479   Climacograptus         <NA>          <NA>
    ## 1059          479   Climacograptus         <NA>          <NA>
    ## 1086          480   Climacograptus         <NA>          <NA>
    ## 1090          480   Climacograptus         <NA>          <NA>
    ## 1101          480   Climacograptus         <NA>          <NA>
    ## 1130          480   Climacograptus         <NA>          <NA>
    ## 1138          480   Climacograptus         <NA>          <NA>
    ## 1163          480   Climacograptus         <NA>          <NA>
    ## 1166          480   Climacograptus         <NA>          <NA>
    ## 1213          480   Climacograptus         <NA>          <NA>
    ## 1215          480   Climacograptus         <NA>          <NA>
    ## 1221          480   Climacograptus         <NA>          <NA>
    ## 1229          480   Climacograptus         <NA>          <NA>
    ## 1247          481   Climacograptus         <NA>          <NA>
    ## 1252          481   Climacograptus         <NA>          <NA>
    ## 1273          481   Climacograptus         <NA>          <NA>
    ## 1285          482   Climacograptus         <NA>          <NA>
    ## 1290          483   Climacograptus         <NA>          <NA>
    ## 1305          482   Climacograptus         <NA>          <NA>
    ## 1309          482   Climacograptus         <NA>          <NA>
    ## 1315          571   Diplograptidae         <NA>          <NA>
    ## 1316          571   Climacograptus         <NA>          <NA>
    ## 1317          571   Climacograptus         <NA>          <NA>
    ## 1360          631   Climacograptus         <NA>          <NA>
    ## 1394          663   Climacograptus         <NA>          <NA>
    ## 1412          622   Climacograptus         <NA>          <NA>
    ## 1416          607   Climacograptus            "          <NA>
    ## 1432          667   Climacograptus         <NA>          <NA>
    ## 1465          623   Climacograptus         <NA>          <NA>
    ## 1473          608   Climacograptus         <NA>          <NA>
    ## 1554         4246   Climacograptus         <NA>          <NA>
    ## 1556         4246   Climacograptus         <NA>          <NA>
    ## 1566         4376   Climacograptus         <NA>          <NA>
    ## 1568         4376   Climacograptus         <NA>          <NA>
    ## 1569         4379   Climacograptus         <NA>          <NA>
    ## 1571         4379   Climacograptus         <NA>          <NA>
    ## 1573         6108   Climacograptus         <NA>          <NA>
    ## 1574         6108   Climacograptus         <NA>          <NA>
    ## 1575         6108   Climacograptus         <NA>          <NA>
    ## 1579         6108   Climacograptus         <NA>          <NA>
    ## 1580         6108   Climacograptus         <NA>          <NA>
    ## 1581         6108   Climacograptus         <NA>          <NA>
    ## 1582         6108   Climacograptus         <NA>          <NA>
    ## 1586         6108   Climacograptus         <NA>          <NA>
    ## 1590         6142   Climacograptus         <NA>          <NA>
    ## 1591         6142   Climacograptus         <NA>          <NA>
    ## 1596         6142   Climacograptus         <NA>          <NA>
    ## 1597         6142   Climacograptus         <NA>          <NA>
    ## 1599         6142   Climacograptus         <NA>          <NA>
    ## 1600         6142   Climacograptus         <NA>          <NA>
    ## 1601         6142   Climacograptus         <NA>          <NA>
    ## 1605         6142   Climacograptus         <NA>          <NA>
    ## 1606         6142   Climacograptus         <NA>          <NA>
    ## 1612         6142   Climacograptus         <NA>          <NA>
    ## 1613         6142   Climacograptus         <NA>          <NA>
    ## 1637         6142   Climacograptus         <NA>          <NA>
    ## 1648         6142   Climacograptus         <NA>          <NA>
    ## 1839         6179   Climacograptus         <NA>          <NA>
    ## 2120          524   Climacograptus         <NA>          <NA>
    ## 2124          524   Climacograptus         <NA>          <NA>
    ## 2128          524   Climacograptus         <NA>          <NA>
    ## 2140          523   Climacograptus         <NA>          <NA>
    ## 2150          523   Climacograptus         <NA>          <NA>
    ## 2166          526   Climacograptus         <NA>          <NA>
    ## 2173          526   Climacograptus         <NA>          <NA>
    ## 2185          526   Climacograptus         <NA>          <NA>
    ## 2192          526   Climacograptus         <NA>          <NA>
    ## 2199          526   Climacograptus         <NA>          <NA>
    ## 2202          526   Climacograptus         <NA>          <NA>
    ## 2211          526   Climacograptus         <NA>          <NA>
    ## 2214          526   Climacograptus         <NA>          <NA>
    ## 2224          526   Climacograptus         <NA>          <NA>
    ## 2234          526   Climacograptus         <NA>          <NA>
    ## 2239          526   Climacograptus         <NA>          <NA>
    ## 2246          526   Climacograptus         <NA>          <NA>
    ## 2256          526   Climacograptus         <NA>          <NA>
    ## 2291         3860   Climacograptus         <NA>          <NA>
    ## 2317         3862   Climacograptus         <NA>          <NA>
    ## 2325         3862   Climacograptus         <NA>          <NA>
    ## 2328         3862   Climacograptus         <NA>          <NA>
    ## 2341         3862   Climacograptus         <NA>          <NA>
    ## 2347         3862   Climacograptus         <NA>          <NA>
    ## 2362         3862   Climacograptus         <NA>          <NA>
    ## 2368         3864   Climacograptus         <NA>          <NA>
    ## 2376         3864   Climacograptus         <NA>          <NA>
    ## 2379         3864   Climacograptus         <NA>          <NA>
    ## 2399         6817   Climacograptus         <NA>          <NA>
    ## 2400         6817   Climacograptus         <NA>          <NA>
    ## 2413         6890   Climacograptus         <NA>          <NA>
    ## 2424         6922   Climacograptus         <NA>          <NA>
    ## 2425         6922   Climacograptus         <NA>          <NA>
    ## 2437         6916   Climacograptus         <NA>          <NA>
    ## 2456         6922   Climacograptus         <NA>          <NA>
    ## 2459         6922   Climacograptus         <NA>          <NA>
    ## 2463         6922   Climacograptus         <NA>          <NA>
    ## 2464         6922   Climacograptus         <NA>          <NA>
    ## 2466         6922   Climacograptus         <NA>          <NA>
    ## 2501         7045   Climacograptus         <NA>          <NA>
    ## 2502         7045   Climacograptus         <NA>          <NA>
    ## 2505         7046   Climacograptus         <NA>          <NA>
    ## 2507         7044   Climacograptus         <NA>          <NA>
    ## 2508         7044   Climacograptus         <NA>          <NA>
    ## 2518         7044   Climacograptus         <NA>          <NA>
    ## 2520         7044   Climacograptus         <NA>          <NA>
    ## 2521         7044   Climacograptus         <NA>          <NA>
    ## 2525         7063   Climacograptus         <NA>          <NA>
    ## 2526         7063   Climacograptus         <NA>          <NA>
    ## 2527         7063   Climacograptus         <NA>          <NA>
    ## 2528         7063   Climacograptus         <NA>          <NA>
    ## 2530         7063   Climacograptus         <NA>          <NA>
    ## 2562         7070   Climacograptus         <NA>          <NA>
    ## 2565         7070   Climacograptus         <NA>          <NA>
    ## 2585         7121   Climacograptus         <NA>          <NA>
    ## 2587         7121   Climacograptus         <NA>          <NA>
    ## 2593         7121   Climacograptus         <NA>          <NA>
    ## 2644         6351   Climacograptus         <NA>          <NA>
    ## 2646         6360   Climacograptus         <NA>          <NA>
    ## 2661         6372   Climacograptus         <NA>          <NA>
    ## 2706         7138   Diplograptidae         <NA>          <NA>
    ## 2707         7138   Climacograptus         <NA>          <NA>
    ## 2708         7138   Climacograptus         <NA>          <NA>
    ## 2710         7138   Climacograptus         <NA>          <NA>
    ## 2755         4261   Climacograptus         <NA>          <NA>
    ## 2793         7251   Climacograptus         <NA>          <NA>
    ## 2797         7251   Climacograptus         <NA>          <NA>
    ## 2798         7251   Climacograptus         <NA>          <NA>
    ## 2799         7251   Climacograptus         <NA>          <NA>
    ## 2804         7251   Climacograptus         <NA>          <NA>
    ## 2806         7251   Climacograptus         <NA>          <NA>
    ## 2807         7251   Climacograptus         <NA>          <NA>
    ## 2809         7251   Climacograptus         <NA>          <NA>
    ## 2810         7251   Climacograptus         <NA>          <NA>
    ## 2884         7455   Climacograptus         <NA>          <NA>
    ## 2891         7455   Climacograptus         <NA>          <NA>
    ## 2892         7455   Climacograptus         <NA>          <NA>
    ## 2893         7455   Climacograptus         <NA>          <NA>
    ## 2934         7455   Climacograptus         <NA>          <NA>
    ## 2935         7455   Climacograptus         <NA>          <NA>
    ## 2943         7455   Climacograptus         <NA>          <NA>
    ## 2948         7455   Climacograptus         <NA>          <NA>
    ## 3021         7455   Climacograptus         <NA>          <NA>
    ## 3108         7624   Climacograptus         <NA>          <NA>
    ## 3110         7624   Climacograptus         <NA>          <NA>
    ## 3116         7624   Climacograptus         <NA>          <NA>
    ## 3127         7624   Climacograptus         <NA>          <NA>
    ## 3128         7624   Climacograptus         <NA>          <NA>
    ## 3129         7624   Climacograptus         <NA>          <NA>
    ## 3148         7624   Climacograptus         <NA>          <NA>
    ## 3149         7624   Climacograptus         <NA>          <NA>
    ## 3173         7624   Climacograptus         <NA>          <NA>
    ## 3182         7624   Climacograptus         <NA>          <NA>
    ## 3199         7624   Climacograptus         <NA>          <NA>
    ## 3200         7624   Climacograptus         <NA>          <NA>
    ## 3202         7624   Climacograptus         <NA>          <NA>
    ## 3246         7624   Climacograptus         <NA>          <NA>
    ## 3248         7624   Climacograptus         <NA>          <NA>
    ## 3276         7624   Climacograptus         <NA>          <NA>
    ## 3290         7624   Climacograptus         <NA>          <NA>
    ## 3318         7624   Climacograptus         <NA>          <NA>
    ## 3353         7624   Climacograptus         <NA>          <NA>
    ## 3358         7624   Climacograptus         <NA>          <NA>
    ## 3366         7624   Climacograptus         <NA>          <NA>
    ## 3377         7624   Climacograptus         <NA>          <NA>
    ## 3386         7624   Climacograptus         <NA>          <NA>
    ## 3403         9363   Climacograptus         <NA>          <NA>
    ## 3462        11462   Climacograptus         <NA>          <NA>
    ## 3473          526   Climacograptus         <NA>          <NA>
    ## 3479          526   Climacograptus         <NA>          <NA>
    ## 3485          526   Climacograptus         <NA>          <NA>
    ## 3530        12470   Climacograptus         <NA>          <NA>
    ## 3541        15106   Climacograptus         <NA>          <NA>
    ## 3545        15106   Climacograptus         <NA>          <NA>
    ## 3677        18179   Climacograptus         <NA>          <NA>
    ## 3842        18179   Climacograptus         <NA>          <NA>
    ## 3847        18179   Diplograptidae         <NA>          <NA>
    ## 3848        18179   Diplograptidae         <NA>          <NA>
    ## 3849        18179   Diplograptidae         <NA>          <NA>
    ## 3857        18179   Diplograptidae         <NA>          <NA>
    ## 3859        18428   Climacograptus         <NA>          <NA>
    ## 3866        18428   Climacograptus         <NA>          <NA>
    ## 3867        18428   Climacograptus         <NA>          <NA>
    ## 3894        18428   Climacograptus         <NA>          <NA>
    ## 3903        18428   Climacograptus         <NA>          <NA>
    ## 3912        18428   Climacograptus         <NA>          <NA>
    ## 3919        18428   Climacograptus         <NA>          <NA>
    ## 3937        18428   Diplograptidae         <NA>          <NA>
    ## 3941        18428   Climacograptus         <NA>          <NA>
    ## 3942        18428   Climacograptus         <NA>          <NA>
    ## 3949        18428   Climacograptus         <NA>          <NA>
    ## 3956        18428   Climacograptus         <NA>          <NA>
    ## 3968        18428   Climacograptus         <NA>          <NA>
    ## 3979        18428   Climacograptus         <NA>          <NA>
    ## 3983        18428   Climacograptus         <NA>          <NA>
    ## 3998        18428   Climacograptus         <NA>          <NA>
    ## 4011        18428   Climacograptus         <NA>          <NA>
    ## 4023        18629   Climacograptus         <NA>          <NA>
    ## 4038        24625   Climacograptus         <NA>          <NA>
    ## 4041        25447   Climacograptus         <NA>          <NA>
    ## 4046        25447   Climacograptus         <NA>          <NA>
    ## 4051        25447 Parareteograptus         <NA>          <NA>
    ## 4061        25780   Climacograptus         <NA>          <NA>
    ## 4062        25780   Climacograptus         <NA>          <NA>
    ## 4067        25780   Climacograptus         <NA>          <NA>
    ## 4072        25807   Climacograptus         <NA>          <NA>
    ## 4075        25807   Climacograptus         <NA>          <NA>
    ## 4096        25968   Climacograptus         <NA>          <NA>
    ## 4097        25968   Climacograptus         <NA>          <NA>
    ## 4099        25968   Climacograptus         <NA>          <NA>
    ## 4101        25968   Climacograptus         <NA>          <NA>
    ## 4102        25968   Climacograptus         <NA>          <NA>
    ## 4104        26007   Climacograptus         <NA>          <NA>
    ## 4110        26007   Climacograptus         <NA>          <NA>
    ## 4113        26007   Climacograptus         <NA>          <NA>
    ## 4115        26007   Climacograptus         <NA>          <NA>
    ## 4138          108   Climacograptus         <NA>          <NA>
    ## 4141        26099   Climacograptus         <NA>          <NA>
    ## 4142        26099   Climacograptus         <NA>          <NA>
    ## 4150        26121   Climacograptus         <NA>          <NA>
    ## 4166        26936   Climacograptus         <NA>          <NA>
    ## 4167        26936   Climacograptus         <NA>          <NA>
    ## 4256        35067   Climacograptus         <NA>          <NA>
    ## 4257        35067   Climacograptus         <NA>          <NA>
    ## 4266        35067   Climacograptus         <NA>          <NA>
    ## 4267        35067   Climacograptus         <NA>          <NA>
    ## 4286        35067   Climacograptus         <NA>          <NA>
    ## 4292        25411   Climacograptus         <NA>          <NA>
    ## 4293        25411   Climacograptus         <NA>          <NA>
    ## 4302        36086   Climacograptus         <NA>          <NA>
    ## 4303        36086   Climacograptus         <NA>          <NA>
    ## 4305        36086   Climacograptus         <NA>          <NA>
    ## 4309        36540   Climacograptus         <NA>          <NA>
    ## 4316        36540   Climacograptus         <NA>          <NA>
    ## 4317        36540   Climacograptus         <NA>          <NA>
    ## 4320        36540   Climacograptus         <NA>          <NA>
    ## 4325        36540   Climacograptus         <NA>          <NA>
    ## 4332        36540   Climacograptus         <NA>          <NA>
    ## 4333        36540   Climacograptus         <NA>          <NA>
    ## 4340        36540   Climacograptus         <NA>          <NA>
    ## 4345        37212   Climacograptus         <NA>          <NA>
    ## 4350        37212   Climacograptus         <NA>          <NA>
    ## 4353        37212   Climacograptus         <NA>          <NA>
    ## 4354        37212   Climacograptus         <NA>          <NA>
    ## 4355        37212   Climacograptus         <NA>          <NA>
    ## 4358        37212   Climacograptus         <NA>          <NA>
    ## 4366        37212   Climacograptus         <NA>          <NA>
    ## 4379        37212   Climacograptus         <NA>          <NA>
    ## 4386        37212   Climacograptus         <NA>          <NA>
    ## 4391        37212   Climacograptus         <NA>          <NA>
    ## 4402        37212   Climacograptus         <NA>          <NA>
    ## 4413        37212   Climacograptus         <NA>          <NA>
    ## 4414        37212   Climacograptus         <NA>          <NA>
    ## 4436        37212   Climacograptus         <NA>          <NA>
    ## 4444        37212   Climacograptus         <NA>          <NA>
    ## 4498        37212   Climacograptus         <NA>          <NA>
    ## 4501        37212   Climacograptus         <NA>          <NA>
    ## 4516        38521   Climacograptus         <NA>          <NA>
    ## 4522        38563   Climacograptus         <NA>          <NA>
    ## 4662        46966   Climacograptus         <NA>          <NA>
    ## 4667        46966   Climacograptus         <NA>          <NA>
    ## 4671        46966   Climacograptus         <NA>          <NA>
    ## 4673        46966   Climacograptus         <NA>          <NA>
    ## 4685        46966   Climacograptus         <NA>          <NA>
    ## 4686        46966   Climacograptus         <NA>          <NA>
    ## 4695        46966   Climacograptus         <NA>          <NA>
    ## 4703        46966   Climacograptus         <NA>          <NA>
    ## 4713        46966   Climacograptus         <NA>          <NA>
    ## 4725        46966   Climacograptus         <NA>          <NA>
    ## 4726        46966   Climacograptus         <NA>          <NA>
    ## 4748        46966   Climacograptus         <NA>          <NA>
    ## 4756        46966   Climacograptus         <NA>          <NA>
    ## 4765        46966   Climacograptus         <NA>          <NA>
    ## 4773        46966   Climacograptus         <NA>          <NA>
    ## 4774        46966   Climacograptus         <NA>          <NA>
    ## 4775        46966   Climacograptus         <NA>          <NA>
    ## 4776        46966   Climacograptus         <NA>          <NA>
    ## 4777        46966   Climacograptus         <NA>          <NA>
    ## 4780        46966   Climacograptus         <NA>          <NA>
    ## 4781        46966   Climacograptus         <NA>          <NA>
    ## 4782        46966   Climacograptus         <NA>          <NA>
    ## 4816        46966   Climacograptus         <NA>          <NA>
    ## 4817        46966   Climacograptus         <NA>          <NA>
    ## 4818        46966   Climacograptus         <NA>          <NA>
    ## 4819        46966   Climacograptus         <NA>          <NA>
    ## 4820        46966   Climacograptus         <NA>          <NA>
    ## 4821        46966   Climacograptus         <NA>          <NA>
    ## 4822        46966   Climacograptus         <NA>          <NA>
    ## 4823        46966   Climacograptus         <NA>          <NA>
    ## 4824        46966   Climacograptus         <NA>          <NA>
    ## 4825        46966   Climacograptus         <NA>          <NA>
    ## 4826        46966   Climacograptus         <NA>          <NA>
    ## 4827        46966   Climacograptus         <NA>          <NA>
    ## 4828        46966   Climacograptus         <NA>          <NA>
    ## 4829        46966   Climacograptus         <NA>          <NA>
    ## 4830        46966   Climacograptus         <NA>          <NA>
    ## 4831        46966   Climacograptus         <NA>          <NA>
    ## 4833        46966   Climacograptus         <NA>          <NA>
    ## 4834        46966   Climacograptus         <NA>          <NA>
    ## 4835        46966   Climacograptus         <NA>          <NA>
    ## 4836        46966   Climacograptus         <NA>          <NA>
    ## 4837        46966   Climacograptus         <NA>          <NA>
    ## 4838        46966   Climacograptus         <NA>          <NA>
    ## 4839        46966   Climacograptus         <NA>          <NA>
    ## 4883        46966   Climacograptus         <NA>          <NA>
    ## 4884        46966   Climacograptus         <NA>          <NA>
    ## 4885        46966   Climacograptus         <NA>          <NA>
    ## 4886        46966   Climacograptus         <NA>          <NA>
    ## 4887        46966   Climacograptus         <NA>          <NA>
    ## 4888        46966   Climacograptus         <NA>          <NA>
    ## 4889        46966   Climacograptus         <NA>          <NA>
    ## 4890        46966   Climacograptus         <NA>          <NA>
    ## 4891        46966   Climacograptus         <NA>          <NA>
    ## 4892        46966   Climacograptus         <NA>          <NA>
    ## 4893        46966   Climacograptus         <NA>          <NA>
    ## 4899        46966   Climacograptus         <NA>          <NA>
    ## 4900        46966   Climacograptus         <NA>          <NA>
    ## 4901        46966   Climacograptus         <NA>          <NA>
    ## 4902        46966   Climacograptus         <NA>          <NA>
    ## 4903        46966   Climacograptus         <NA>          <NA>
    ## 4904        46966   Climacograptus         <NA>          <NA>
    ## 4905        46966   Climacograptus         <NA>          <NA>
    ## 4906        46966   Climacograptus         <NA>          <NA>
    ## 4907        46966   Climacograptus         <NA>          <NA>
    ## 4908        46966   Climacograptus         <NA>          <NA>
    ## 4909        46966   Climacograptus         <NA>          <NA>
    ## 4910        46966   Climacograptus         <NA>          <NA>
    ## 4911        46966   Climacograptus         <NA>          <NA>
    ## 4912        46966   Climacograptus         <NA>          <NA>
    ## 4913        46966   Climacograptus         <NA>          <NA>
    ## 4914        46966   Climacograptus         <NA>          <NA>
    ## 4915        46966   Climacograptus         <NA>          <NA>
    ## 4916        46966   Climacograptus         <NA>          <NA>
    ## 4917        46966   Climacograptus         <NA>          <NA>
    ## 4918        46966   Climacograptus         <NA>          <NA>
    ## 4919        46966   Climacograptus         <NA>          <NA>
    ## 4920        46966   Climacograptus         <NA>          <NA>
    ## 4921        46966   Climacograptus         <NA>          <NA>
    ## 4923        46966   Climacograptus         <NA>          <NA>
    ## 4924        46966   Climacograptus         <NA>          <NA>
    ## 4925        46966   Climacograptus         <NA>          <NA>
    ## 4926        46966   Climacograptus         <NA>          <NA>
    ## 4927        46966   Climacograptus         <NA>          <NA>
    ## 4928        46966   Climacograptus         <NA>          <NA>
    ## 4929        46966   Climacograptus         <NA>          <NA>
    ## 4962        46966   Climacograptus         <NA>          <NA>
    ## 4963        46966   Climacograptus         <NA>          <NA>
    ## 4964        46966   Climacograptus         <NA>          <NA>
    ## 5102        47076   Climacograptus         <NA>          <NA>
    ## 5103        47076   Climacograptus         <NA>          <NA>
    ## 5106        47076   Climacograptus         <NA>          <NA>
    ## 5110        47076   Climacograptus         <NA>          <NA>
    ## 5114        47076   Climacograptus         <NA>          <NA>
    ## 5115        47076   Climacograptus         <NA>          <NA>
    ## 5126        47076   Climacograptus         <NA>          <NA>
    ## 5127        47076   Climacograptus         <NA>          <NA>
    ## 5128        47076   Climacograptus         <NA>          <NA>
    ## 5129        47076   Climacograptus         <NA>          <NA>
    ## 5130        47076   Climacograptus         <NA>          <NA>
    ## 5131        47076   Climacograptus         <NA>          <NA>
    ## 5132        47076   Climacograptus         <NA>          <NA>
    ## 5150        47076   Climacograptus         <NA>          <NA>
    ## 5151        47076   Climacograptus         <NA>          <NA>
    ## 5152        47076   Climacograptus         <NA>          <NA>
    ## 5153        47076   Climacograptus         <NA>          <NA>
    ## 5154        47076   Climacograptus         <NA>          <NA>
    ## 5155        47076   Climacograptus         <NA>          <NA>
    ## 5167        47076   Climacograptus         <NA>          <NA>
    ## 5176        47076   Climacograptus         <NA>          <NA>
    ## 5177        47076   Climacograptus         <NA>          <NA>
    ## 5195        47076   Climacograptus         <NA>          <NA>
    ## 5204        47083   Climacograptus         <NA>          <NA>
    ## 5205        47083   Climacograptus         <NA>          <NA>
    ## 5248        47087       Anticostia         <NA>          <NA>
    ## 5249        47087       Anticostia         <NA>          <NA>
    ## 5250        47087       Anticostia         <NA>          <NA>
    ## 5251        47087       Anticostia         <NA>          <NA>
    ## 5253        47087   Climacograptus         <NA>          <NA>
    ## 5256        47087 Parareteograptus         <NA>          <NA>
    ## 5260        47087     Rectograptus         <NA>          <NA>
    ## 5261        47087       Anticostia         <NA>          <NA>
    ## 5262        47087       Anticostia         <NA>          <NA>
    ## 5263        47087       Anticostia         <NA>          <NA>
    ## 5265        47087   Climacograptus         <NA>          <NA>
    ## 5268        47087 Parareteograptus         <NA>          <NA>
    ## 5270        47087     Rectograptus         <NA>          <NA>
    ## 5275        47087       Anticostia         <NA>          <NA>
    ## 5277        47087   Climacograptus         <NA>          <NA>
    ## 5281        47087 Parareteograptus         <NA>          <NA>
    ## 5286        47087       Anticostia         <NA>          <NA>
    ## 5287        47087       Anticostia         <NA>          <NA>
    ## 5289        47087   Climacograptus         <NA>          <NA>
    ## 5293        47087 Parareteograptus         <NA>          <NA>
    ## 5298        47087       Anticostia         <NA>          <NA>
    ## 5299        47087       Anticostia         <NA>          <NA>
    ## 5300        47087       Anticostia         <NA>          <NA>
    ## 5301        47087       Anticostia         <NA>          <NA>
    ## 5302        47087       Anticostia         <NA>          <NA>
    ## 5305        47087   Climacograptus         <NA>          <NA>
    ## 5306        47087   Climacograptus         <NA>          <NA>
    ## 5307        47087   Climacograptus         <NA>          <NA>
    ## 5314        47087 Parareteograptus         <NA>          <NA>
    ## 5315        47087 Parareteograptus         <NA>          <NA>
    ## 5319        47087       Anticostia         <NA>          <NA>
    ## 5320        47087       Anticostia         <NA>          <NA>
    ## 5322        47087     Rectograptus         <NA>          <NA>
    ## 5323        47087     Rectograptus         <NA>          <NA>
    ## 5326        47087       Anticostia         <NA>          <NA>
    ## 5327        47087       Anticostia         <NA>          <NA>
    ## 5330        47089   Climacograptus         <NA>          <NA>
    ## 5333        47089   Climacograptus         <NA>          <NA>
    ## 5342        47103   Climacograptus         <NA>          <NA>
    ## 5343        47103   Climacograptus         <NA>          <NA>
    ## 5344        47103   Climacograptus         <NA>          <NA>
    ## 5345        47103   Climacograptus         <NA>          <NA>
    ## 5346        47103   Climacograptus         <NA>          <NA>
    ## 5347        47103   Climacograptus         <NA>          <NA>
    ## 5353        47103   Climacograptus         <NA>          <NA>
    ## 5354        47103   Climacograptus         <NA>          <NA>
    ## 5355        47103   Climacograptus         <NA>          <NA>
    ## 5363        47103   Climacograptus         <NA>          <NA>
    ## 5364        47103   Climacograptus         <NA>          <NA>
    ## 5365        47103   Climacograptus         <NA>          <NA>
    ## 5385        47103   Climacograptus         <NA>          <NA>
    ## 5486        47087       Anticostia         <NA>          <NA>
    ## 5487        47087       Anticostia         <NA>          <NA>
    ## 5488        47087       Anticostia         <NA>          <NA>
    ## 5490        47087   Climacograptus         <NA>          <NA>
    ## 5495        47087 Parareteograptus         <NA>          <NA>
    ## 5496        47087     Rectograptus         <NA>          <NA>
    ## 5506        47087       Anticostia         <NA>          <NA>
    ## 5508        47087   Climacograptus         <NA>          <NA>
    ## 5513        47087 Parareteograptus         <NA>          <NA>
    ## 5515        47087     Rectograptus         <NA>          <NA>
    ## 5518        47087       Anticostia         <NA>          <NA>
    ## 5523        47087 Parareteograptus         <NA>          <NA>
    ## 5524        47087       Anticostia         <NA>          <NA>
    ## 5525        47087   Climacograptus         <NA>          <NA>
    ## 5530        47087 Parareteograptus         <NA>          <NA>
    ## 5532        47087     Rectograptus         <NA>          <NA>
    ## 5538        47087       Anticostia         <NA>          <NA>
    ## 5544        47087 Parareteograptus         <NA>          <NA>
    ## 5547        47087 Parareteograptus         <NA>          <NA>
    ## 5548        47087       Anticostia         <NA>          <NA>
    ## 5549        47087   Climacograptus         <NA>          <NA>
    ## 5554        47087     Rectograptus         <NA>          <NA>
    ## 5559        47087       Anticostia         <NA>          <NA>
    ## 5563        47087 Parareteograptus         <NA>          <NA>
    ## 5565        47087 Parareteograptus         <NA>          <NA>
    ## 5567        47087       Anticostia         <NA>          <NA>
    ## 5568        47087   Climacograptus         <NA>          <NA>
    ## 5573        47087 Parareteograptus         <NA>          <NA>
    ## 5575        47087     Rectograptus         <NA>          <NA>
    ## 5585        47087       Anticostia         <NA>          <NA>
    ## 5586        47087       Anticostia         <NA>          <NA>
    ## 5587        47087       Anticostia         <NA>          <NA>
    ## 5588        47087   Climacograptus         <NA>          <NA>
    ## 5593        47087     Rectograptus         <NA>          <NA>
    ## 5598        47087       Anticostia         <NA>          <NA>
    ## 5599        47087   Climacograptus         <NA>          <NA>
    ## 5602        47087     Rectograptus         <NA>          <NA>
    ## 5606        47087       Anticostia         <NA>          <NA>
    ## 5607        47087   Climacograptus         <NA>          <NA>
    ## 5610        47087 Parareteograptus         <NA>          <NA>
    ## 5611        47087     Rectograptus         <NA>          <NA>
    ## 5613        47087       Anticostia         <NA>          <NA>
    ## 5616        47087       Anticostia         <NA>          <NA>
    ## 5617        47087       Anticostia         <NA>          <NA>
    ## 5621        47087     Rectograptus         <NA>          <NA>
    ## 5625        47087       Anticostia         <NA>          <NA>
    ## 5631        47087       Anticostia         <NA>          <NA>
    ## 5632        47087       Anticostia         <NA>          <NA>
    ## 5633        47087   Climacograptus         <NA>          <NA>
    ## 5637        47087     Rectograptus         <NA>          <NA>
    ## 5641        47087       Anticostia         <NA>          <NA>
    ## 5646        47087       Anticostia         <NA>          <NA>
    ## 5670        47087     Rectograptus         <NA>          <NA>
    ## 5673        47087       Anticostia         <NA>          <NA>
    ## 5719        47087   Climacograptus         <NA>          <NA>
    ## 5724        47087 Parareteograptus         <NA>          <NA>
    ## 5726        47087     Rectograptus         <NA>          <NA>
    ## 5727        47087   Climacograptus         <NA>          <NA>
    ## 5731        47087     Rectograptus         <NA>          <NA>
    ## 5732        47087       Anticostia         <NA>          <NA>
    ## 5735        47087   Climacograptus         <NA>          <NA>
    ## 5740        47087 Parareteograptus         <NA>          <NA>
    ## 5742        47087     Rectograptus         <NA>          <NA>
    ## 5743        47087       Anticostia         <NA>          <NA>
    ## 5745        47087       Anticostia         <NA>          <NA>
    ## 5747        47087 Parareteograptus         <NA>          <NA>
    ## 5748        47087   Climacograptus         <NA>          <NA>
    ## 5752        47087 Parareteograptus         <NA>          <NA>
    ## 5754        47087     Rectograptus         <NA>          <NA>
    ## 5760        47087   Climacograptus         <NA>          <NA>
    ## 5764        47087 Parareteograptus         <NA>          <NA>
    ## 5766        47087     Rectograptus         <NA>          <NA>
    ## 5776        47087   Climacograptus         <NA>          <NA>
    ## 5783        47087     Rectograptus         <NA>          <NA>
    ## 5843        49361     Rectograptus         <NA>          <NA>
    ## 5845        49367   Climacograptus         <NA>          <NA>
    ## 5871        52096   Climacograptus         <NA>          <NA>
    ## 5886          119   Climacograptus         <NA>          <NA>
    ## 5892          102   Climacograptus         <NA>          <NA>
    ## 5896           78   Climacograptus         <NA>          <NA>
    ##      subgenus_reso         species_name species_reso subgenus subgenus_no
    ## 32            <NA>                  sp.         <NA>       NA          NA
    ## 39            <NA>                  sp.         <NA>       NA          NA
    ## 56            <NA>                  sp.         <NA>       NA          NA
    ## 58            <NA>                  sp.         <NA>       NA          NA
    ## 66            <NA>                  sp.         <NA>       NA          NA
    ## 74            <NA>                  sp.         <NA>       NA          NA
    ## 77            <NA>                  sp.         <NA>       NA          NA
    ## 83            <NA>                  sp.         <NA>       NA          NA
    ## 89            <NA>                  sp.         <NA>       NA          NA
    ## 94            <NA>                  sp.         <NA>       NA          NA
    ## 105           <NA>                  sp.         <NA>       NA          NA
    ## 110           <NA>                  sp.         <NA>       NA          NA
    ## 115           <NA>                  sp.         <NA>       NA          NA
    ## 117           <NA>                  sp.         <NA>       NA          NA
    ## 120           <NA>                  sp.         <NA>       NA          NA
    ## 122           <NA>                  sp.         <NA>       NA          NA
    ## 128           <NA>                  sp.         <NA>       NA          NA
    ## 131           <NA>                  sp.         <NA>       NA          NA
    ## 152           <NA>                  sp.         <NA>       NA          NA
    ## 156           <NA>                  sp.         <NA>       NA          NA
    ## 181           <NA>                  sp.         <NA>       NA          NA
    ## 192           <NA>                  sp.         <NA>       NA          NA
    ## 194           <NA>                  sp.         <NA>       NA          NA
    ## 214           <NA>                  sp.         <NA>       NA          NA
    ## 226           <NA>                  sp.         <NA>       NA          NA
    ## 233           <NA>             scalaris         <NA>       NA          NA
    ## 234           <NA>            innotatus         <NA>       NA          NA
    ## 236           <NA>             scalaris         <NA>       NA          NA
    ## 237           <NA>            innotatus         <NA>       NA          NA
    ## 257           <NA>                  sp.         <NA>       NA          NA
    ## 259           <NA>                  sp.         <NA>       NA          NA
    ## 261           <NA>                  sp.         <NA>       NA          NA
    ## 264           <NA>                  sp.         <NA>       NA          NA
    ## 267           <NA>                  sp.         <NA>       NA          NA
    ## 269           <NA>                  sp.         <NA>       NA          NA
    ## 273           <NA>                  sp.         <NA>       NA          NA
    ## 276           <NA>                  sp.         <NA>       NA          NA
    ## 283           <NA>                  sp.         <NA>       NA          NA
    ## 294           <NA>                  sp.         <NA>       NA          NA
    ## 298           <NA>                  sp.         <NA>       NA          NA
    ## 303           <NA>                  sp.         <NA>       NA          NA
    ## 312           <NA>                  sp.         <NA>       NA          NA
    ## 400           <NA>                  sp.         <NA>       NA          NA
    ## 411           <NA>                  sp.         <NA>       NA          NA
    ## 415           <NA>                  sp.         <NA>       NA          NA
    ## 416           <NA>                  sp.         <NA>       NA          NA
    ## 418           <NA>                  sp.         <NA>       NA          NA
    ## 422           <NA>                  sp.         <NA>       NA          NA
    ## 436           <NA>         scharenbergi         <NA>       NA          NA
    ## 444           <NA>                  sp.         <NA>       NA          NA
    ## 472           <NA>                  sp.         <NA>       NA          NA
    ## 482           <NA>                  sp.         <NA>       NA          NA
    ## 489           <NA>                  sp.         <NA>       NA          NA
    ## 493           <NA>                  sp.         <NA>       NA          NA
    ## 502           <NA>                  sp.         <NA>       NA          NA
    ## 511           <NA>                  sp.         <NA>       NA          NA
    ## 523           <NA>                  sp.         <NA>       NA          NA
    ## 529           <NA>                  sp.         <NA>       NA          NA
    ## 534           <NA>                  sp.         <NA>       NA          NA
    ## 544           <NA>                  sp.         <NA>       NA          NA
    ## 549           <NA>                  sp.         <NA>       NA          NA
    ## 553           <NA>                  sp.         <NA>       NA          NA
    ## 560           <NA>                  sp.         <NA>       NA          NA
    ## 571           <NA>                  sp.         <NA>       NA          NA
    ## 579           <NA>                  sp.         <NA>       NA          NA
    ## 586           <NA>                  sp.         <NA>       NA          NA
    ## 587           <NA>                  sp.         <NA>       NA          NA
    ## 627           <NA>                  sp.         <NA>       NA          NA
    ## 634           <NA>                  sp.         <NA>       NA          NA
    ## 641           <NA>                  sp.         <NA>       NA          NA
    ## 659           <NA>                  sp.         <NA>       NA          NA
    ## 665           <NA>                  sp.         <NA>       NA          NA
    ## 666           <NA>                  sp.         <NA>       NA          NA
    ## 670           <NA>                  sp.         <NA>       NA          NA
    ## 698           <NA>                  sp.         <NA>       NA          NA
    ## 706           <NA>                  sp.         <NA>       NA          NA
    ## 725           <NA>                  sp.         <NA>       NA          NA
    ## 729           <NA>                  sp.         <NA>       NA          NA
    ## 734           <NA>                  sp.         <NA>       NA          NA
    ## 738           <NA>                  sp.         <NA>       NA          NA
    ## 741           <NA>                  sp.         <NA>       NA          NA
    ## 746           <NA>                  sp.         <NA>       NA          NA
    ## 759           <NA>                  sp.         <NA>       NA          NA
    ## 791           <NA>                  sp.         <NA>       NA          NA
    ## 795           <NA>                  sp.         <NA>       NA          NA
    ## 808           <NA>                  sp.         <NA>       NA          NA
    ## 813           <NA>                  sp.         <NA>       NA          NA
    ## 819           <NA>                  sp.         <NA>       NA          NA
    ## 837           <NA>                  sp.         <NA>       NA          NA
    ## 865           <NA>                  sp.         <NA>       NA          NA
    ## 887           <NA>                  sp.         <NA>       NA          NA
    ## 891           <NA>                  sp.         <NA>       NA          NA
    ## 918           <NA>                  sp.         <NA>       NA          NA
    ## 920           <NA>                  sp.         <NA>       NA          NA
    ## 923           <NA>                  sp.         <NA>       NA          NA
    ## 929           <NA>                  sp.         <NA>       NA          NA
    ## 933           <NA>                  sp.         <NA>       NA          NA
    ## 949           <NA>                  sp.         <NA>       NA          NA
    ## 960           <NA>                  sp.         <NA>       NA          NA
    ## 968           <NA>                  sp.         <NA>       NA          NA
    ## 1000          <NA>                  sp.         <NA>       NA          NA
    ## 1003          <NA>                  sp.         <NA>       NA          NA
    ## 1012          <NA>                  sp.         <NA>       NA          NA
    ## 1016          <NA>                  sp.         <NA>       NA          NA
    ## 1027          <NA>                  sp.         <NA>       NA          NA
    ## 1059          <NA>                  sp.         <NA>       NA          NA
    ## 1086          <NA>                  sp.         <NA>       NA          NA
    ## 1090          <NA>                  sp.         <NA>       NA          NA
    ## 1101          <NA>                  sp.         <NA>       NA          NA
    ## 1130          <NA>                  sp.         <NA>       NA          NA
    ## 1138          <NA>                  sp.         <NA>       NA          NA
    ## 1163          <NA>                  sp.         <NA>       NA          NA
    ## 1166          <NA>                  sp.         <NA>       NA          NA
    ## 1213          <NA>                  sp.         <NA>       NA          NA
    ## 1215          <NA>                  sp.         <NA>       NA          NA
    ## 1221          <NA>                  sp.         <NA>       NA          NA
    ## 1229          <NA>                  sp.         <NA>       NA          NA
    ## 1247          <NA>                  sp.         <NA>       NA          NA
    ## 1252          <NA>                  sp.         <NA>       NA          NA
    ## 1273          <NA>                  sp.         <NA>       NA          NA
    ## 1285          <NA>                  sp.         <NA>       NA          NA
    ## 1290          <NA>                  sp.         <NA>       NA          NA
    ## 1305          <NA>                  sp.         <NA>       NA          NA
    ## 1309          <NA>                  sp.         <NA>       NA          NA
    ## 1315          <NA>               indet.         <NA>       NA          NA
    ## 1316          <NA>          miserabilis          cf.       NA          NA
    ## 1317          <NA>                  sp.         <NA>       NA          NA
    ## 1360          <NA>                  sp.         <NA>       NA          NA
    ## 1394          <NA>                  sp.         <NA>       NA          NA
    ## 1412          <NA>                  sp.         <NA>       NA          NA
    ## 1416          <NA>                  sp.         <NA>       NA          NA
    ## 1432          <NA>                  sp.         <NA>       NA          NA
    ## 1465          <NA>                  sp.         <NA>       NA          NA
    ## 1473          <NA>                  sp.         <NA>       NA          NA
    ## 1554          <NA> rectangulares-medius         <NA>       NA          NA
    ## 1556          <NA> rectangularis-medius         <NA>       NA          NA
    ## 1566          <NA>                  sp.         <NA>       NA          NA
    ## 1568          <NA>     C. rectangularis          cf.       NA          NA
    ## 1569          <NA>            typicalis         <NA>       NA          NA
    ## 1571          <NA>              pumilis         <NA>       NA          NA
    ## 1573          <NA>          tubuliferus         <NA>       NA          NA
    ## 1574          <NA>             caudatus         <NA>       NA          NA
    ## 1575          <NA>            innotatus         <NA>       NA          NA
    ## 1579          <NA>             caudatus         <NA>       NA          NA
    ## 1580          <NA>            innotatus         <NA>       NA          NA
    ## 1581          <NA>              minimus          cf.       NA          NA
    ## 1582          <NA>          tubuliferus         <NA>       NA          NA
    ## 1586          <NA>            uncinatus            ?       NA          NA
    ## 1590          <NA>             angustus         <NA>       NA          NA
    ## 1591          <NA>          miserabilis         <NA>       NA          NA
    ## 1596          <NA>             angustus         <NA>       NA          NA
    ## 1597          <NA>               medius         <NA>       NA          NA
    ## 1599          <NA>        rectangularis         <NA>       NA          NA
    ## 1600          <NA>             angustus         <NA>       NA          NA
    ## 1601          <NA>               medius         <NA>       NA          NA
    ## 1605          <NA>        rectangularis         <NA>       NA          NA
    ## 1606          <NA>             balticus         <NA>       NA          NA
    ## 1612          <NA>        rectangularis         <NA>       NA          NA
    ## 1613          <NA>             scalaris            ?       NA          NA
    ## 1637          <NA>             scalaris            ?       NA          NA
    ## 1648          <NA>             scalaris            ?       NA          NA
    ## 1839          <NA>               medius          cf.       NA          NA
    ## 2120          <NA>                  sp.         <NA>       NA          NA
    ## 2124          <NA>                  sp.         <NA>       NA          NA
    ## 2128          <NA>                  sp.         <NA>       NA          NA
    ## 2140          <NA>                  sp.         <NA>       NA          NA
    ## 2150          <NA>                  sp.         <NA>       NA          NA
    ## 2166          <NA>                  sp.         <NA>       NA          NA
    ## 2173          <NA>                  sp.         <NA>       NA          NA
    ## 2185          <NA>                  sp.         <NA>       NA          NA
    ## 2192          <NA>                  sp.         <NA>       NA          NA
    ## 2199          <NA>                  sp.         <NA>       NA          NA
    ## 2202          <NA>                  sp.         <NA>       NA          NA
    ## 2211          <NA>                  sp.         <NA>       NA          NA
    ## 2214          <NA>                  sp.         <NA>       NA          NA
    ## 2224          <NA>                  sp.         <NA>       NA          NA
    ## 2234          <NA>                  sp.         <NA>       NA          NA
    ## 2239          <NA>                  sp.         <NA>       NA          NA
    ## 2246          <NA>                  sp.         <NA>       NA          NA
    ## 2256          <NA>                  sp.         <NA>       NA          NA
    ## 2291          <NA>                  sp.         <NA>       NA          NA
    ## 2317          <NA>                  sp.         <NA>       NA          NA
    ## 2325          <NA>                  sp.         <NA>       NA          NA
    ## 2328          <NA>                  sp.         <NA>       NA          NA
    ## 2341          <NA>                  sp.         <NA>       NA          NA
    ## 2347          <NA>                  sp.         <NA>       NA          NA
    ## 2362          <NA>                  sp.         <NA>       NA          NA
    ## 2368          <NA>                  sp.         <NA>       NA          NA
    ## 2376          <NA>                  sp.         <NA>       NA          NA
    ## 2379          <NA>                  sp.         <NA>       NA          NA
    ## 2399          <NA>             bicornis         <NA>       NA          NA
    ## 2400          <NA>               inuiti         <NA>       NA          NA
    ## 2413          <NA>             venustus         <NA>       NA          NA
    ## 2424          <NA>            typicalis         <NA>       NA          NA
    ## 2425          <NA>            dorotheus         <NA>       NA          NA
    ## 2437          <NA>             scalaris         aff.       NA          NA
    ## 2456          <NA>                  sp.         <NA>       NA          NA
    ## 2459          <NA>        rectangularis         <NA>       NA          NA
    ## 2463          <NA>               medius         <NA>       NA          NA
    ## 2464          <NA>        rectangularis         <NA>       NA          NA
    ## 2466          <NA>               medius         <NA>       NA          NA
    ## 2501          <NA>            innotatus         <NA>       NA          NA
    ## 2502          <NA>        rectangularis          cf.       NA          NA
    ## 2505          <NA>              minutus          cf.       NA          NA
    ## 2507          <NA>            typicalis         <NA>       NA          NA
    ## 2508          <NA>          spiniferous         <NA>       NA          NA
    ## 2518          <NA>             angustus         <NA>       NA          NA
    ## 2520          <NA>             venustus         <NA>       NA          NA
    ## 2521          <NA>                  sp.         <NA>       NA          NA
    ## 2525          <NA>             supernus         <NA>       NA          NA
    ## 2526          <NA>             hvalross         <NA>       NA          NA
    ## 2527          <NA>             hastatus         <NA>       NA          NA
    ## 2528          <NA>         raricaudatus          cf.       NA          NA
    ## 2530          <NA>             scalaris         <NA>       NA          NA
    ## 2562          <NA>             bicornis          cf.       NA          NA
    ## 2565          <NA>             bicornis          cf.       NA          NA
    ## 2585          <NA>                  sp.         <NA>       NA          NA
    ## 2587          <NA>                  sp.         <NA>       NA          NA
    ## 2593          <NA>                  sp.         <NA>       NA          NA
    ## 2644          <NA>                  sp.         <NA>       NA          NA
    ## 2646          <NA>                  sp.         <NA>       NA          NA
    ## 2661          <NA>                  sp.         <NA>       NA          NA
    ## 2706          <NA>               indet.         <NA>       NA          NA
    ## 2707          <NA>            innotatus         <NA>       NA          NA
    ## 2708          <NA>            innotatus         <NA>       NA          NA
    ## 2710          <NA>                  sp.         <NA>       NA          NA
    ## 2755          <NA>                  sp.         <NA>       NA          NA
    ## 2793          <NA>                  sp.         <NA>       NA          NA
    ## 2797          <NA>              aqualis         <NA>       NA          NA
    ## 2798          <NA>           prolificus         <NA>       NA          NA
    ## 2799          <NA>            typicalis         <NA>       NA          NA
    ## 2804          <NA>            typicalis         <NA>       NA          NA
    ## 2806          <NA>            typicalis         <NA>       NA          NA
    ## 2807          <NA>            typicalis         <NA>       NA          NA
    ## 2809          <NA>           prolificus         <NA>       NA          NA
    ## 2810          <NA>            rougensis         <NA>       NA          NA
    ## 2884          <NA>             scalaris         <NA>       NA          NA
    ## 2891          <NA>                  sp.         <NA>       NA          NA
    ## 2892          <NA>            bohemicus          cf.       NA          NA
    ## 2893          <NA>         yangtseensis         <NA>       NA          NA
    ## 2934          <NA>             scalaris          cf.       NA          NA
    ## 2935          <NA>        rectangularis          cf.       NA          NA
    ## 2943          <NA>               medius         <NA>       NA          NA
    ## 2948          <NA>             scalaris         <NA>       NA          NA
    ## 3021          <NA>             scalaris          cf.       NA          NA
    ## 3108          <NA>              minutus          cf.       NA          NA
    ## 3110          <NA>             angustus         <NA>       NA          NA
    ## 3116          <NA>                  sp.         <NA>       NA          NA
    ## 3127          <NA>             angustus         <NA>       NA          NA
    ## 3128          <NA>              minutus         <NA>       NA          NA
    ## 3129          <NA>        rectangularis          cf.       NA          NA
    ## 3148          <NA>         yangtzeensis         <NA>       NA          NA
    ## 3149          <NA>               medius         <NA>       NA          NA
    ## 3173          <NA>             scalaris         <NA>       NA          NA
    ## 3182          <NA>               medius         <NA>       NA          NA
    ## 3199          <NA>           mirnyensis         <NA>       NA          NA
    ## 3200          <NA>             angustus         <NA>       NA          NA
    ## 3202          <NA>                  sp.         <NA>       NA          NA
    ## 3246          <NA>             scalaris         <NA>       NA          NA
    ## 3248          <NA>        rectangularis         <NA>       NA          NA
    ## 3276          <NA>                  sp.         <NA>       NA          NA
    ## 3290          <NA>        tangshanensis         <NA>       NA          NA
    ## 3318          <NA>                  sp.         <NA>       NA          NA
    ## 3353          <NA>          yangtzensis          cf.       NA          NA
    ## 3358          <NA>                  sp.         <NA>       NA          NA
    ## 3366          <NA>             supernus         <NA>       NA          NA
    ## 3377          <NA>                  sp.         <NA>       NA          NA
    ## 3386          <NA>        rectangulatus         <NA>       NA          NA
    ## 3403          <NA>            typicalis         <NA>       NA          NA
    ## 3462          <NA>                  sp.         <NA>       NA          NA
    ## 3473          <NA>                  sp.         <NA>       NA          NA
    ## 3479          <NA>                  sp.         <NA>       NA          NA
    ## 3485          <NA>                  sp.         <NA>       NA          NA
    ## 3530          <NA>          tubuliferus         aff.       NA          NA
    ## 3541          <NA>                  sp.         <NA>       NA          NA
    ## 3545          <NA>                  sp.         <NA>       NA          NA
    ## 3677          <NA>               brevis         <NA>       NA          NA
    ## 3842          <NA>                  sp.         <NA>       NA          NA
    ## 3847          <NA>               indet.         <NA>       NA          NA
    ## 3848          <NA>               indet.         <NA>       NA          NA
    ## 3849          <NA>               indet.         <NA>       NA          NA
    ## 3857          <NA>               indet.         <NA>       NA          NA
    ## 3859          <NA>             antiquus         <NA>       NA          NA
    ## 3866          <NA>             antiquus         <NA>       NA          NA
    ## 3867          <NA>                  sp.         <NA>       NA          NA
    ## 3894          <NA>             antiquus         <NA>       NA          NA
    ## 3903          <NA>             antiquus         <NA>       NA          NA
    ## 3912          <NA>             antiquus         <NA>       NA          NA
    ## 3919          <NA>                  sp.         <NA>       NA          NA
    ## 3937          <NA>               indet.         <NA>       NA          NA
    ## 3941          <NA>                  sp.         <NA>       NA          NA
    ## 3942          <NA>             antiquus         <NA>       NA          NA
    ## 3949          <NA>             antiquus          cf.       NA          NA
    ## 3956          <NA>             antiquus          cf.       NA          NA
    ## 3968          <NA>             antiquus         <NA>       NA          NA
    ## 3979          <NA>                  sp.         <NA>       NA          NA
    ## 3983          <NA>             antiquus         <NA>       NA          NA
    ## 3998          <NA>             antiquus          cf.       NA          NA
    ## 4011          <NA>             antiquus         <NA>       NA          NA
    ## 4023          <NA>             angustus         <NA>       NA          NA
    ## 4038          <NA>                  sp.         <NA>       NA          NA
    ## 4041          <NA>           angustatus         <NA>       NA          NA
    ## 4046          <NA>                  sp.         <NA>       NA          NA
    ## 4051          <NA>                  sp.         <NA>       NA          NA
    ## 4061          <NA>              minimus          cf.       NA          NA
    ## 4062          <NA>           styloideus         <NA>       NA          NA
    ## 4067          <NA>              minimus          cf.       NA          NA
    ## 4072          <NA>                  sp.         <NA>       NA          NA
    ## 4075          <NA>                  sp.         <NA>       NA          NA
    ## 4096          <NA>                  sp.         <NA>       NA          NA
    ## 4097          <NA>            typicalis         <NA>       NA          NA
    ## 4099          <NA>            typicalis         <NA>       NA          NA
    ## 4101          <NA>                  sp.         <NA>       NA          NA
    ## 4102          <NA>            typicalis         <NA>       NA          NA
    ## 4104          <NA>               brevis         <NA>       NA          NA
    ## 4110          <NA>                  sp.         <NA>       NA          NA
    ## 4113          <NA>         scharenbergi         <NA>       NA          NA
    ## 4115          <NA>                  sp.         <NA>       NA          NA
    ## 4138          <NA>                  sp.         <NA>       NA          NA
    ## 4141          <NA>              minimus         <NA>       NA          NA
    ## 4142          <NA>           styloideus         <NA>       NA          NA
    ## 4150          <NA>          tridentatus         <NA>       NA          NA
    ## 4166          <NA>             bicornis         <NA>       NA          NA
    ## 4167          <NA>                  sp.         <NA>       NA          NA
    ## 4256          <NA>         riddellensis         <NA>       NA          NA
    ## 4257          <NA>                  sp.         <NA>       NA          NA
    ## 4266          <NA>         riddellensis         <NA>       NA          NA
    ## 4267          <NA>         scharenbergi          cf.       NA          NA
    ## 4286          <NA>                  sp.         <NA>       NA          NA
    ## 4292          <NA>         phyllophorus          cf.       NA          NA
    ## 4293          <NA>         phyllophorus          cf.       NA          NA
    ## 4302          <NA>                latus         <NA>       NA          NA
    ## 4303          <NA>                latus         <NA>       NA          NA
    ## 4305          <NA>                latus         <NA>       NA          NA
    ## 4309          <NA>              pungens         <NA>       NA          NA
    ## 4316          <NA>                  sp.         <NA>       NA          NA
    ## 4317          <NA>                  sp.         <NA>       NA          NA
    ## 4320          <NA>             bicornis         <NA>       NA          NA
    ## 4325          <NA>             bicornis         <NA>       NA          NA
    ## 4332          <NA>             bicornis         <NA>       NA          NA
    ## 4333          <NA>              eximius          cf.       NA          NA
    ## 4340          <NA>                  sp.         <NA>       NA          NA
    ## 4345          <NA>                  sp.         <NA>       NA          NA
    ## 4350          <NA>                  sp.         <NA>       NA          NA
    ## 4353          <NA>              hughesi          cf.       NA          NA
    ## 4354          <NA>             scalaris          cf.       NA          NA
    ## 4355          <NA>                  sp.         <NA>       NA          NA
    ## 4358          <NA>                  sp.         <NA>       NA          NA
    ## 4366          <NA>                  sp.         <NA>       NA          NA
    ## 4379          <NA>                  sp.         <NA>       NA          NA
    ## 4386          <NA>                  sp.         <NA>       NA          NA
    ## 4391          <NA>                  sp.         <NA>       NA          NA
    ## 4402          <NA>             antiquus         aff.       NA          NA
    ## 4413          <NA>         phyllophorus          cf.       NA          NA
    ## 4414          <NA>                  sp.         <NA>       NA          NA
    ## 4436          <NA>                  sp.         <NA>       NA          NA
    ## 4444          <NA>                  sp.         <NA>       NA          NA
    ## 4498          <NA>                  sp.         <NA>       NA          NA
    ## 4501          <NA>                  sp.         <NA>       NA          NA
    ## 4516          <NA>             bicornis         <NA>       NA          NA
    ## 4522          <NA>               brevis         <NA>       NA          NA
    ## 4662          <NA>                  sp.         <NA>       NA          NA
    ## 4667          <NA>                  sp.         <NA>       NA          NA
    ## 4671          <NA>                  sp.         <NA>       NA          NA
    ## 4673          <NA>                  sp.         <NA>       NA          NA
    ## 4685          <NA>             bicornis         <NA>       NA          NA
    ## 4686          <NA>               brevis         <NA>       NA          NA
    ## 4695          <NA>             bicornis         <NA>       NA          NA
    ## 4703          <NA>             bicornis         <NA>       NA          NA
    ## 4713          <NA>             bicornis         <NA>       NA          NA
    ## 4725          <NA>             bicornis         <NA>       NA          NA
    ## 4726          <NA>         riddellensis         <NA>       NA          NA
    ## 4748          <NA>                  sp.         <NA>       NA          NA
    ## 4756          <NA>                  sp.         <NA>       NA          NA
    ## 4765          <NA>                  sp.         <NA>       NA          NA
    ## 4773          <NA>             bicornis         <NA>       NA          NA
    ## 4774          <NA>             bicornis         <NA>       NA          NA
    ## 4775          <NA>             bicornis          cf.       NA          NA
    ## 4776          <NA>         raricaudatus          cf.       NA          NA
    ## 4777          <NA>          tubuliferus          cf.       NA          NA
    ## 4780          <NA>                  sp.         <NA>       NA          NA
    ## 4781          <NA>                  sp.         <NA>       NA          NA
    ## 4782          <NA>                  sp.         <NA>       NA          NA
    ## 4816          <NA>             caudatus         <NA>       NA          NA
    ## 4817          <NA>             caudatus         <NA>       NA          NA
    ## 4818          <NA>             caudatus         <NA>       NA          NA
    ## 4819          <NA>             caudatus         <NA>       NA          NA
    ## 4820          <NA>            innotatus         <NA>       NA          NA
    ## 4821          <NA>            innotatus         <NA>       NA          NA
    ## 4822          <NA>          mohawkensis          cf.       NA          NA
    ## 4823          <NA>          mohawkensis          cf.       NA          NA
    ## 4824          <NA>          tubuliferus         <NA>       NA          NA
    ## 4825          <NA>          tubuliferus         <NA>       NA          NA
    ## 4826          <NA>          tubuliferus         <NA>       NA          NA
    ## 4827          <NA>          tubuliferus         <NA>       NA          NA
    ## 4828          <NA>          tubuliferus         <NA>       NA          NA
    ## 4829          <NA>          tubuliferus         <NA>       NA          NA
    ## 4830          <NA>          tubuliferus         <NA>       NA          NA
    ## 4831          <NA>          tubuliferus         <NA>       NA          NA
    ## 4833          <NA>                  sp.         <NA>       NA          NA
    ## 4834          <NA>                  sp.         <NA>       NA          NA
    ## 4835          <NA>                  sp.         <NA>       NA          NA
    ## 4836          <NA>                  sp.         <NA>       NA          NA
    ## 4837          <NA>                  sp.         <NA>       NA          NA
    ## 4838          <NA>                  sp.         <NA>       NA          NA
    ## 4839          <NA>                  sp.         <NA>       NA          NA
    ## 4883          <NA>             hastatus            ?       NA          NA
    ## 4884          <NA>             hastatus         <NA>       NA          NA
    ## 4885          <NA>             hastatus         <NA>       NA          NA
    ## 4886          <NA>             hastatus         <NA>       NA          NA
    ## 4887          <NA>             hastatus         <NA>       NA          NA
    ## 4888          <NA>             hastatus         <NA>       NA          NA
    ## 4889          <NA>          longispinus         <NA>       NA          NA
    ## 4890          <NA>          longispinus         <NA>       NA          NA
    ## 4891          <NA>          longispinus         <NA>       NA          NA
    ## 4892          <NA>          longispinus         <NA>       NA          NA
    ## 4893          <NA>          longispinus         <NA>       NA          NA
    ## 4899          <NA>          mohawkensis          cf.       NA          NA
    ## 4900          <NA>          mohawkensis          cf.       NA          NA
    ## 4901          <NA>          mohawkensis          cf.       NA          NA
    ## 4902          <NA>          mohawkensis          cf.       NA          NA
    ## 4903          <NA>            pacificus         <NA>       NA          NA
    ## 4904          <NA>            pacificus         <NA>       NA          NA
    ## 4905          <NA>            pacificus         <NA>       NA          NA
    ## 4906          <NA>          tabuliferus          cf.       NA          NA
    ## 4907          <NA>          tabuliferus          cf.       NA          NA
    ## 4908          <NA>          tabuliferus          cf.       NA          NA
    ## 4909          <NA>          tabuliferus          cf.       NA          NA
    ## 4910          <NA>          tabuliferus          cf.       NA          NA
    ## 4911          <NA>            uncinatus         <NA>       NA          NA
    ## 4912          <NA>            uncinatus         <NA>       NA          NA
    ## 4913          <NA>            uncinatus         <NA>       NA          NA
    ## 4914          <NA>            uncinatus         <NA>       NA          NA
    ## 4915          <NA>            uncinatus         <NA>       NA          NA
    ## 4916          <NA>            uncinatus         <NA>       NA          NA
    ## 4917          <NA>                sp. A     informal       NA          NA
    ## 4918          <NA>                sp. A     informal       NA          NA
    ## 4919          <NA>                sp. A     informal       NA          NA
    ## 4920          <NA>                sp. A     informal       NA          NA
    ## 4921          <NA>                sp. A     informal       NA          NA
    ## 4923          <NA>                sp. A     informal       NA          NA
    ## 4924          <NA>                sp. A     informal       NA          NA
    ## 4925          <NA>                latus         aff.       NA          NA
    ## 4926          <NA>                  sp.         <NA>       NA          NA
    ## 4927          <NA>                  sp.         <NA>       NA          NA
    ## 4928          <NA>                  sp.         <NA>       NA          NA
    ## 4929          <NA>                  sp.         <NA>       NA          NA
    ## 4962          <NA>             scalaris          cf.       NA          NA
    ## 4963          <NA>             scalaris          cf.       NA          NA
    ## 4964          <NA>                  sp.         <NA>       NA          NA
    ## 5102          <NA>               medius          cf.       NA          NA
    ## 5103          <NA>             trifilis         <NA>       NA          NA
    ## 5106          <NA>               medius          cf.       NA          NA
    ## 5110          <NA>               medius          cf.       NA          NA
    ## 5114          <NA>            innotatus         <NA>       NA          NA
    ## 5115          <NA>             scalaris         <NA>       NA          NA
    ## 5126          <NA>            indivisus         <NA>       NA          NA
    ## 5127          <NA>            innotatus         <NA>       NA          NA
    ## 5128          <NA>               medius          cf.       NA          NA
    ## 5129          <NA>              minutus            ?       NA          NA
    ## 5130          <NA>        rectangularis          cf.       NA          NA
    ## 5131          <NA>        rectangularis         <NA>       NA          NA
    ## 5132          <NA>             scalaris         <NA>       NA          NA
    ## 5150          <NA>            innotatus         <NA>       NA          NA
    ## 5151          <NA>               medius          cf.       NA          NA
    ## 5152          <NA>        rectangularis          cf.       NA          NA
    ## 5153          <NA>        rectangularis         <NA>       NA          NA
    ## 5154          <NA>             scalaris         <NA>       NA          NA
    ## 5155          <NA>             trifilis         <NA>       NA          NA
    ## 5167          <NA>           stenotelus         <NA>       NA          NA
    ## 5176          <NA>               medius         <NA>       NA          NA
    ## 5177          <NA>        rectangularis          cf.       NA          NA
    ## 5195          <NA>               medius          cf.       NA          NA
    ## 5204          <NA>             scalaris         <NA>       NA          NA
    ## 5205          <NA>        rectangularis         <NA>       NA          NA
    ## 5248          <NA>           tenuissima         <NA>       NA          NA
    ## 5249          <NA>                 lata         <NA>       NA          NA
    ## 5250          <NA>       thorsteinssoni         <NA>       NA          NA
    ## 5251          <NA>           fastigiata         <NA>       NA          NA
    ## 5253          <NA>             hastatus         <NA>       NA          NA
    ## 5256          <NA>             sinensis         <NA>       NA          NA
    ## 5260          <NA>          abbreviatus         <NA>       NA          NA
    ## 5261          <NA>                 lata         <NA>       NA          NA
    ## 5262          <NA>            fastigata         <NA>       NA          NA
    ## 5263          <NA>           tenuissima         <NA>       NA          NA
    ## 5265          <NA>             hastatus         <NA>       NA          NA
    ## 5268          <NA>             sinensis         <NA>       NA          NA
    ## 5270          <NA>          abbreviatus         <NA>       NA          NA
    ## 5275          <NA>            festigata         <NA>       NA          NA
    ## 5277          <NA>             hastatus         <NA>       NA          NA
    ## 5281          <NA>             sinensis         <NA>       NA          NA
    ## 5286          <NA>                 lata         <NA>       NA          NA
    ## 5287          <NA>            fastigata         <NA>       NA          NA
    ## 5289          <NA>             hastatus         <NA>       NA          NA
    ## 5293          <NA>             sinensis         <NA>       NA          NA
    ## 5298          <NA>                 lata         <NA>       NA          NA
    ## 5299          <NA>                 lata         <NA>       NA          NA
    ## 5300          <NA>            fastigata         <NA>       NA          NA
    ## 5301          <NA>            fastigata         <NA>       NA          NA
    ## 5302          <NA>            fastigata         <NA>       NA          NA
    ## 5305          <NA>             hastatus         <NA>       NA          NA
    ## 5306          <NA>             hastatus         <NA>       NA          NA
    ## 5307          <NA>             hastatus         <NA>       NA          NA
    ## 5314          <NA>             sinensis         <NA>       NA          NA
    ## 5315          <NA>             sinensis         <NA>       NA          NA
    ## 5319          <NA>           tenuissima         <NA>       NA          NA
    ## 5320          <NA>           tenuissima         <NA>       NA          NA
    ## 5322          <NA>          abbreviatus         <NA>       NA          NA
    ## 5323          <NA>          abbreviatus         <NA>       NA          NA
    ## 5326          <NA>            uniformis         <NA>       NA          NA
    ## 5327          <NA>            uniformis         <NA>       NA          NA
    ## 5330          <NA>             bicornis         <NA>       NA          NA
    ## 5333          <NA>               brevis         <NA>       NA          NA
    ## 5342          <NA>                  sp.         <NA>       NA          NA
    ## 5343          <NA>               medius         <NA>       NA          NA
    ## 5344          <NA>             scalaris         <NA>       NA          NA
    ## 5345          <NA>        rectangularis         <NA>       NA          NA
    ## 5346          <NA>             trifilis         <NA>       NA          NA
    ## 5347          <NA>                  sp.         <NA>       NA          NA
    ## 5353          <NA>           longespina         <NA>       NA          NA
    ## 5354          <NA>               medius         <NA>       NA          NA
    ## 5355          <NA>             scalaris         <NA>       NA          NA
    ## 5363          <NA>           longespina         <NA>       NA          NA
    ## 5364          <NA>               medius         <NA>       NA          NA
    ## 5365          <NA>             scalaris         <NA>       NA          NA
    ## 5385          <NA>             scalaris         <NA>       NA          NA
    ## 5486          <NA>                 lata         <NA>       NA          NA
    ## 5487          <NA>            fastigata         <NA>       NA          NA
    ## 5488          <NA>           tenuissima         <NA>       NA          NA
    ## 5490          <NA>             hastatus         <NA>       NA          NA
    ## 5495          <NA>             sinensis         <NA>       NA          NA
    ## 5496          <NA>          abbreviatus         <NA>       NA          NA
    ## 5506          <NA>                 lata         <NA>       NA          NA
    ## 5508          <NA>             hastatus         <NA>       NA          NA
    ## 5513          <NA>             sinensis         <NA>       NA          NA
    ## 5515          <NA>          abbreviatus         <NA>       NA          NA
    ## 5518          <NA>            uniformis         <NA>       NA          NA
    ## 5523          <NA>               parvus         <NA>       NA          NA
    ## 5524          <NA>                 lata         <NA>       NA          NA
    ## 5525          <NA>             hastatus         <NA>       NA          NA
    ## 5530          <NA>             sinensis         <NA>       NA          NA
    ## 5532          <NA>          abbreviatus         <NA>       NA          NA
    ## 5538          <NA>            uniformis         <NA>       NA          NA
    ## 5544          <NA>               parvus         <NA>       NA          NA
    ## 5547          <NA>             turgidus         <NA>       NA          NA
    ## 5548          <NA>                 lata         <NA>       NA          NA
    ## 5549          <NA>             hastatus         <NA>       NA          NA
    ## 5554          <NA>          abbreviatus         <NA>       NA          NA
    ## 5559          <NA>            uniformis         <NA>       NA          NA
    ## 5563          <NA>               parvus         <NA>       NA          NA
    ## 5565          <NA>             turgidus         <NA>       NA          NA
    ## 5567          <NA>                 lata         <NA>       NA          NA
    ## 5568          <NA>             hastatus         <NA>       NA          NA
    ## 5573          <NA>             sinensis         <NA>       NA          NA
    ## 5575          <NA>          abbreviatus         <NA>       NA          NA
    ## 5585          <NA>          macgregorae         <NA>       NA          NA
    ## 5586          <NA>                 lata         <NA>       NA          NA
    ## 5587          <NA>            fastigata         <NA>       NA          NA
    ## 5588          <NA>             hastatus         <NA>       NA          NA
    ## 5593          <NA>          abbreviatus         <NA>       NA          NA
    ## 5598          <NA>                 lata         <NA>       NA          NA
    ## 5599          <NA>             hastatus         <NA>       NA          NA
    ## 5602          <NA>          abbreviatus         <NA>       NA          NA
    ## 5606          <NA>                 lata         <NA>       NA          NA
    ## 5607          <NA>             hastatus         <NA>       NA          NA
    ## 5610          <NA>             sinensis         <NA>       NA          NA
    ## 5611          <NA>          abbreviatus         <NA>       NA          NA
    ## 5613          <NA>            uniformis         <NA>       NA          NA
    ## 5616          <NA>                 lata         <NA>       NA          NA
    ## 5617          <NA>            fastigata         <NA>       NA          NA
    ## 5621          <NA>          abbreviatus         <NA>       NA          NA
    ## 5625          <NA>            uniformis         <NA>       NA          NA
    ## 5631          <NA>                 lata         <NA>       NA          NA
    ## 5632          <NA>            fastigata         <NA>       NA          NA
    ## 5633          <NA>             hastatus         <NA>       NA          NA
    ## 5637          <NA>          abbreviatus         <NA>       NA          NA
    ## 5641          <NA>            uniformis         <NA>       NA          NA
    ## 5646          <NA>          macgregorae         <NA>       NA          NA
    ## 5670          <NA>          abbreviatus         <NA>       NA          NA
    ## 5673          <NA>            uniformis         <NA>       NA          NA
    ## 5719          <NA>             hastatus         <NA>       NA          NA
    ## 5724          <NA>             sinensis         <NA>       NA          NA
    ## 5726          <NA>          abbreviatus         <NA>       NA          NA
    ## 5727          <NA>             hastatus         <NA>       NA          NA
    ## 5731          <NA>          abbreviatus         <NA>       NA          NA
    ## 5732          <NA>                 lata         <NA>       NA          NA
    ## 5735          <NA>             hastatus         <NA>       NA          NA
    ## 5740          <NA>             sinensis         <NA>       NA          NA
    ## 5742          <NA>          abbreviatus         <NA>       NA          NA
    ## 5743          <NA>                 lata         <NA>       NA          NA
    ## 5745          <NA>           tenuissima         <NA>       NA          NA
    ## 5747          <NA>               parvus         <NA>       NA          NA
    ## 5748          <NA>             hastatus         <NA>       NA          NA
    ## 5752          <NA>             sinensis         <NA>       NA          NA
    ## 5754          <NA>          abbreviatus         <NA>       NA          NA
    ## 5760          <NA>             hastatus         <NA>       NA          NA
    ## 5764          <NA>             sinensis         <NA>       NA          NA
    ## 5766          <NA>          abbreviatus         <NA>       NA          NA
    ## 5776          <NA>             hastatus         <NA>       NA          NA
    ## 5783          <NA>          abbreviatus         <NA>       NA          NA
    ## 5843          <NA>          abbreviatus         <NA>       NA          NA
    ## 5845          <NA>            indivisus          cf.       NA          NA
    ## 5871          <NA>             scalaris         <NA>       NA          NA
    ## 5886          <NA>           styloideus         <NA>       NA          NA
    ## 5892          <NA>             antiquus         <NA>       NA          NA
    ## 5896          <NA>             scalaris         <NA>       NA          NA
    ##                 genus genus_no         family family_no        order
    ## 32     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 39     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 56     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 58     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 66     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 74     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 77     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 83     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 89     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 94     Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 105    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 110    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 115    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 117    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 120    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 122    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 128    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 131    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 152    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 156    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 181    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 192    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 194    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 214    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 226    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 233    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 234    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 236    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 237    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 257    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 259    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 261    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 264    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 267    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 269    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 273    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 276    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 283    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 294    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 298    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 303    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 312    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 400    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 411    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 415      Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 416    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 418      Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 422      Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 436    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 444    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 472    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 482    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 489    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 493    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 502    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 511    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 523    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 529    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 534    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 544    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 549    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 553    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 560    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 571    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 579    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 586    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 587    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 627    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 634    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 641    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 659    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 665    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 666    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 670    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 698    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 706    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 725    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 729    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 734    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 738    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 741    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 746    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 759    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 791    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 795    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 808    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 813    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 819    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 837    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 865    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 887    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 891    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 918    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 920    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 923    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 929    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 933    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 949    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 960    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 968    Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1000   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1003   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1012   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1016   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1027   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1059   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1086   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1090   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1101   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1130   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1138   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1163   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1166   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1213   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1215   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1221   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1229   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1247   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1252   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1273   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1285   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1290   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1305   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1309   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1315             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 1316   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1317   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1360   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1394   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1412   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1416   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1432   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1465   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1473   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1554   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1556   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1566   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1568   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1569   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1571   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1573   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1574   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1575   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1579   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1580   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1581   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1582   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1586   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1590   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1591   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1596   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1597   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1599   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1600   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1601   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1605   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1606   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1612   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1613   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1637   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1648   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 1839   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2120   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2124   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2128   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2140   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2150   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2166   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2173   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2185   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2192   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2199   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2202   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2211   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2214   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2224   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2234   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2239   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2246   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2256   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2291   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2317   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2325   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2328   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2341   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2347   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2362   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2368   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2376   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2379   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2399   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2400   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2413   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2424   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2425   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2437   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2456   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2459   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2463   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2464   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2466   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2501   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2502   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2505   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2507   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2508   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2518   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2520   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2521   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2525   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2526   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2527   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2528   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2530   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2562   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2565   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2585   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2587   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2593   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2644   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2646   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2661   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2706             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 2707   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2708   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2710   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2755   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2793   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2797   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2798   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2799   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2804   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2806   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2807   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2809   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2810   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2884   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2891   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2892   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2893   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2934   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2935   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2943   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 2948   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3021   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3108   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3110   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3116   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3127   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3128   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3129   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3148   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3149   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3173   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3182   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3199   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3200   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3202   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3246   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3248   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3276   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3290   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3318   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3353   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3358   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3366   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3377   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3386   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3403   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3462   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3473   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3479   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3485   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3530   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3541   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3545   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3677   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3842   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3847             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 3848             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 3849             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 3857             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 3859   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3866   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3867   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3894   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3903   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3912   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3919   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3937             <NA>       NA Diplograptidae    150197 Graptoloidea
    ## 3941   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3942   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3949   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3956   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3968   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3979   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3983   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 3998   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4011   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4023   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4038   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4041   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4046   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4051 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 4061   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4062   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4067   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4072   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4075   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4096   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4097   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4099   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4101   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4102   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4104   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4110   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4113   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4115   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4138   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4141   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4142   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4150   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4166   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4167   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4256   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4257   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4266   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4267   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4286   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4292   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4293   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4302   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4303   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4305   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4309   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4316   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4317   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4320   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4325   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4332   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4333   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4340   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4345   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4350   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4353   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4354   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4355   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4358   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4366   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4379   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4386   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4391   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4402   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4413   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4414   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4436   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4444   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4498   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4501   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4516   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4522   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4662   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4667   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4671   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4673   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4685   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4686   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4695   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4703   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4713   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4725   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4726   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4748   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4756   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4765   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4773   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4774   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4775   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4776   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4777   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4780   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4781   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4782   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4816   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4817   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4818   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4819   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4820   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4821   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4822   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4823   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4824   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4825   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4826   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4827   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4828   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4829   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4830   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4831   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4833   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4834   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4835   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4836   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4837   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4838   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4839   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4883   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4884   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4885   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4886   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4887   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4888   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4889   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4890   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4891   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4892   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4893   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4899   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4900   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4901   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4902   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4903   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4904   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4905   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4906   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4907   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4908   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4909   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4910   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4911   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4912   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4913   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4914   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4915   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4916   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4917   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4918   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4919   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4920   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4921   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4923   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4924   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4925   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4926   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4927   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4928   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4929   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4962   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4963   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 4964   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5102   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5103   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5106   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5110   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5114   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5115   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5126   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5127   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5128   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5129   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5130   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5131   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5132   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5150   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5151   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5152   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5153   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5154   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5155   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5167   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5176   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5177   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5195   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5204   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5205   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5248       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5249       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5250       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5251       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5253   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5256 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5260     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5261       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5262       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5263       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5265   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5268 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5270     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5275       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5277   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5281 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5286       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5287       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5289   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5293 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5298       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5299       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5300       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5301       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5302       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5305   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5306   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5307   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5314 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5315 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5319       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5320       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5322     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5323     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5326       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5327       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5330   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5333   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5342   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5343   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5344   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5345   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5346   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5347   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5353   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5354   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5355   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5363   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5364   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5365   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5385   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5486       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5487       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5488       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5490   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5495 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5496     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5506       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5508   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5513 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5515     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5518       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5523 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5524       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5525   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5530 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5532     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5538       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5544 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5547 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5548       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5549   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5554     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5559       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5563 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5565 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5567       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5568   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5573 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5575     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5585       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5586       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5587       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5588   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5593     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5598       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5599   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5602     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5606       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5607   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5610 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5611     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5613       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5616       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5617       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5621     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5625       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5631       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5632       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5633   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5637     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5641       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5646       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5670     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5673       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5719   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5724 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5726     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5727   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5731     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5732       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5735   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5740 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5742     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5743       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5745       Anticostia   270341 Diplograptidae    150197 Graptoloidea
    ## 5747 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5748   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5752 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5754     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5760   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5764 Parareteograptus   270338 Diplograptidae    150197 Graptoloidea
    ## 5766     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5776   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5783     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5843     Rectograptus   270339 Diplograptidae    150197 Graptoloidea
    ## 5845   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5871   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5886   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5892   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ## 5896   Climacograptus    33636 Diplograptidae    150197 Graptoloidea
    ##      order_no         class class_no       phylum phylum_no
    ## 32      33606 Graptolithina    33534 Hemichordata     33518
    ## 39      33606 Graptolithina    33534 Hemichordata     33518
    ## 56      33606 Graptolithina    33534 Hemichordata     33518
    ## 58      33606 Graptolithina    33534 Hemichordata     33518
    ## 66      33606 Graptolithina    33534 Hemichordata     33518
    ## 74      33606 Graptolithina    33534 Hemichordata     33518
    ## 77      33606 Graptolithina    33534 Hemichordata     33518
    ## 83      33606 Graptolithina    33534 Hemichordata     33518
    ## 89      33606 Graptolithina    33534 Hemichordata     33518
    ## 94      33606 Graptolithina    33534 Hemichordata     33518
    ## 105     33606 Graptolithina    33534 Hemichordata     33518
    ## 110     33606 Graptolithina    33534 Hemichordata     33518
    ## 115     33606 Graptolithina    33534 Hemichordata     33518
    ## 117     33606 Graptolithina    33534 Hemichordata     33518
    ## 120     33606 Graptolithina    33534 Hemichordata     33518
    ## 122     33606 Graptolithina    33534 Hemichordata     33518
    ## 128     33606 Graptolithina    33534 Hemichordata     33518
    ## 131     33606 Graptolithina    33534 Hemichordata     33518
    ## 152     33606 Graptolithina    33534 Hemichordata     33518
    ## 156     33606 Graptolithina    33534 Hemichordata     33518
    ## 181     33606 Graptolithina    33534 Hemichordata     33518
    ## 192     33606 Graptolithina    33534 Hemichordata     33518
    ## 194     33606 Graptolithina    33534 Hemichordata     33518
    ## 214     33606 Graptolithina    33534 Hemichordata     33518
    ## 226     33606 Graptolithina    33534 Hemichordata     33518
    ## 233     33606 Graptolithina    33534 Hemichordata     33518
    ## 234     33606 Graptolithina    33534 Hemichordata     33518
    ## 236     33606 Graptolithina    33534 Hemichordata     33518
    ## 237     33606 Graptolithina    33534 Hemichordata     33518
    ## 257     33606 Graptolithina    33534 Hemichordata     33518
    ## 259     33606 Graptolithina    33534 Hemichordata     33518
    ## 261     33606 Graptolithina    33534 Hemichordata     33518
    ## 264     33606 Graptolithina    33534 Hemichordata     33518
    ## 267     33606 Graptolithina    33534 Hemichordata     33518
    ## 269     33606 Graptolithina    33534 Hemichordata     33518
    ## 273     33606 Graptolithina    33534 Hemichordata     33518
    ## 276     33606 Graptolithina    33534 Hemichordata     33518
    ## 283     33606 Graptolithina    33534 Hemichordata     33518
    ## 294     33606 Graptolithina    33534 Hemichordata     33518
    ## 298     33606 Graptolithina    33534 Hemichordata     33518
    ## 303     33606 Graptolithina    33534 Hemichordata     33518
    ## 312     33606 Graptolithina    33534 Hemichordata     33518
    ## 400     33606 Graptolithina    33534 Hemichordata     33518
    ## 411     33606 Graptolithina    33534 Hemichordata     33518
    ## 415     33606 Graptolithina    33534 Hemichordata     33518
    ## 416     33606 Graptolithina    33534 Hemichordata     33518
    ## 418     33606 Graptolithina    33534 Hemichordata     33518
    ## 422     33606 Graptolithina    33534 Hemichordata     33518
    ## 436     33606 Graptolithina    33534 Hemichordata     33518
    ## 444     33606 Graptolithina    33534 Hemichordata     33518
    ## 472     33606 Graptolithina    33534 Hemichordata     33518
    ## 482     33606 Graptolithina    33534 Hemichordata     33518
    ## 489     33606 Graptolithina    33534 Hemichordata     33518
    ## 493     33606 Graptolithina    33534 Hemichordata     33518
    ## 502     33606 Graptolithina    33534 Hemichordata     33518
    ## 511     33606 Graptolithina    33534 Hemichordata     33518
    ## 523     33606 Graptolithina    33534 Hemichordata     33518
    ## 529     33606 Graptolithina    33534 Hemichordata     33518
    ## 534     33606 Graptolithina    33534 Hemichordata     33518
    ## 544     33606 Graptolithina    33534 Hemichordata     33518
    ## 549     33606 Graptolithina    33534 Hemichordata     33518
    ## 553     33606 Graptolithina    33534 Hemichordata     33518
    ## 560     33606 Graptolithina    33534 Hemichordata     33518
    ## 571     33606 Graptolithina    33534 Hemichordata     33518
    ## 579     33606 Graptolithina    33534 Hemichordata     33518
    ## 586     33606 Graptolithina    33534 Hemichordata     33518
    ## 587     33606 Graptolithina    33534 Hemichordata     33518
    ## 627     33606 Graptolithina    33534 Hemichordata     33518
    ## 634     33606 Graptolithina    33534 Hemichordata     33518
    ## 641     33606 Graptolithina    33534 Hemichordata     33518
    ## 659     33606 Graptolithina    33534 Hemichordata     33518
    ## 665     33606 Graptolithina    33534 Hemichordata     33518
    ## 666     33606 Graptolithina    33534 Hemichordata     33518
    ## 670     33606 Graptolithina    33534 Hemichordata     33518
    ## 698     33606 Graptolithina    33534 Hemichordata     33518
    ## 706     33606 Graptolithina    33534 Hemichordata     33518
    ## 725     33606 Graptolithina    33534 Hemichordata     33518
    ## 729     33606 Graptolithina    33534 Hemichordata     33518
    ## 734     33606 Graptolithina    33534 Hemichordata     33518
    ## 738     33606 Graptolithina    33534 Hemichordata     33518
    ## 741     33606 Graptolithina    33534 Hemichordata     33518
    ## 746     33606 Graptolithina    33534 Hemichordata     33518
    ## 759     33606 Graptolithina    33534 Hemichordata     33518
    ## 791     33606 Graptolithina    33534 Hemichordata     33518
    ## 795     33606 Graptolithina    33534 Hemichordata     33518
    ## 808     33606 Graptolithina    33534 Hemichordata     33518
    ## 813     33606 Graptolithina    33534 Hemichordata     33518
    ## 819     33606 Graptolithina    33534 Hemichordata     33518
    ## 837     33606 Graptolithina    33534 Hemichordata     33518
    ## 865     33606 Graptolithina    33534 Hemichordata     33518
    ## 887     33606 Graptolithina    33534 Hemichordata     33518
    ## 891     33606 Graptolithina    33534 Hemichordata     33518
    ## 918     33606 Graptolithina    33534 Hemichordata     33518
    ## 920     33606 Graptolithina    33534 Hemichordata     33518
    ## 923     33606 Graptolithina    33534 Hemichordata     33518
    ## 929     33606 Graptolithina    33534 Hemichordata     33518
    ## 933     33606 Graptolithina    33534 Hemichordata     33518
    ## 949     33606 Graptolithina    33534 Hemichordata     33518
    ## 960     33606 Graptolithina    33534 Hemichordata     33518
    ## 968     33606 Graptolithina    33534 Hemichordata     33518
    ## 1000    33606 Graptolithina    33534 Hemichordata     33518
    ## 1003    33606 Graptolithina    33534 Hemichordata     33518
    ## 1012    33606 Graptolithina    33534 Hemichordata     33518
    ## 1016    33606 Graptolithina    33534 Hemichordata     33518
    ## 1027    33606 Graptolithina    33534 Hemichordata     33518
    ## 1059    33606 Graptolithina    33534 Hemichordata     33518
    ## 1086    33606 Graptolithina    33534 Hemichordata     33518
    ## 1090    33606 Graptolithina    33534 Hemichordata     33518
    ## 1101    33606 Graptolithina    33534 Hemichordata     33518
    ## 1130    33606 Graptolithina    33534 Hemichordata     33518
    ## 1138    33606 Graptolithina    33534 Hemichordata     33518
    ## 1163    33606 Graptolithina    33534 Hemichordata     33518
    ## 1166    33606 Graptolithina    33534 Hemichordata     33518
    ## 1213    33606 Graptolithina    33534 Hemichordata     33518
    ## 1215    33606 Graptolithina    33534 Hemichordata     33518
    ## 1221    33606 Graptolithina    33534 Hemichordata     33518
    ## 1229    33606 Graptolithina    33534 Hemichordata     33518
    ## 1247    33606 Graptolithina    33534 Hemichordata     33518
    ## 1252    33606 Graptolithina    33534 Hemichordata     33518
    ## 1273    33606 Graptolithina    33534 Hemichordata     33518
    ## 1285    33606 Graptolithina    33534 Hemichordata     33518
    ## 1290    33606 Graptolithina    33534 Hemichordata     33518
    ## 1305    33606 Graptolithina    33534 Hemichordata     33518
    ## 1309    33606 Graptolithina    33534 Hemichordata     33518
    ## 1315    33606 Graptolithina    33534 Hemichordata     33518
    ## 1316    33606 Graptolithina    33534 Hemichordata     33518
    ## 1317    33606 Graptolithina    33534 Hemichordata     33518
    ## 1360    33606 Graptolithina    33534 Hemichordata     33518
    ## 1394    33606 Graptolithina    33534 Hemichordata     33518
    ## 1412    33606 Graptolithina    33534 Hemichordata     33518
    ## 1416    33606 Graptolithina    33534 Hemichordata     33518
    ## 1432    33606 Graptolithina    33534 Hemichordata     33518
    ## 1465    33606 Graptolithina    33534 Hemichordata     33518
    ## 1473    33606 Graptolithina    33534 Hemichordata     33518
    ## 1554    33606 Graptolithina    33534 Hemichordata     33518
    ## 1556    33606 Graptolithina    33534 Hemichordata     33518
    ## 1566    33606 Graptolithina    33534 Hemichordata     33518
    ## 1568    33606 Graptolithina    33534 Hemichordata     33518
    ## 1569    33606 Graptolithina    33534 Hemichordata     33518
    ## 1571    33606 Graptolithina    33534 Hemichordata     33518
    ## 1573    33606 Graptolithina    33534 Hemichordata     33518
    ## 1574    33606 Graptolithina    33534 Hemichordata     33518
    ## 1575    33606 Graptolithina    33534 Hemichordata     33518
    ## 1579    33606 Graptolithina    33534 Hemichordata     33518
    ## 1580    33606 Graptolithina    33534 Hemichordata     33518
    ## 1581    33606 Graptolithina    33534 Hemichordata     33518
    ## 1582    33606 Graptolithina    33534 Hemichordata     33518
    ## 1586    33606 Graptolithina    33534 Hemichordata     33518
    ## 1590    33606 Graptolithina    33534 Hemichordata     33518
    ## 1591    33606 Graptolithina    33534 Hemichordata     33518
    ## 1596    33606 Graptolithina    33534 Hemichordata     33518
    ## 1597    33606 Graptolithina    33534 Hemichordata     33518
    ## 1599    33606 Graptolithina    33534 Hemichordata     33518
    ## 1600    33606 Graptolithina    33534 Hemichordata     33518
    ## 1601    33606 Graptolithina    33534 Hemichordata     33518
    ## 1605    33606 Graptolithina    33534 Hemichordata     33518
    ## 1606    33606 Graptolithina    33534 Hemichordata     33518
    ## 1612    33606 Graptolithina    33534 Hemichordata     33518
    ## 1613    33606 Graptolithina    33534 Hemichordata     33518
    ## 1637    33606 Graptolithina    33534 Hemichordata     33518
    ## 1648    33606 Graptolithina    33534 Hemichordata     33518
    ## 1839    33606 Graptolithina    33534 Hemichordata     33518
    ## 2120    33606 Graptolithina    33534 Hemichordata     33518
    ## 2124    33606 Graptolithina    33534 Hemichordata     33518
    ## 2128    33606 Graptolithina    33534 Hemichordata     33518
    ## 2140    33606 Graptolithina    33534 Hemichordata     33518
    ## 2150    33606 Graptolithina    33534 Hemichordata     33518
    ## 2166    33606 Graptolithina    33534 Hemichordata     33518
    ## 2173    33606 Graptolithina    33534 Hemichordata     33518
    ## 2185    33606 Graptolithina    33534 Hemichordata     33518
    ## 2192    33606 Graptolithina    33534 Hemichordata     33518
    ## 2199    33606 Graptolithina    33534 Hemichordata     33518
    ## 2202    33606 Graptolithina    33534 Hemichordata     33518
    ## 2211    33606 Graptolithina    33534 Hemichordata     33518
    ## 2214    33606 Graptolithina    33534 Hemichordata     33518
    ## 2224    33606 Graptolithina    33534 Hemichordata     33518
    ## 2234    33606 Graptolithina    33534 Hemichordata     33518
    ## 2239    33606 Graptolithina    33534 Hemichordata     33518
    ## 2246    33606 Graptolithina    33534 Hemichordata     33518
    ## 2256    33606 Graptolithina    33534 Hemichordata     33518
    ## 2291    33606 Graptolithina    33534 Hemichordata     33518
    ## 2317    33606 Graptolithina    33534 Hemichordata     33518
    ## 2325    33606 Graptolithina    33534 Hemichordata     33518
    ## 2328    33606 Graptolithina    33534 Hemichordata     33518
    ## 2341    33606 Graptolithina    33534 Hemichordata     33518
    ## 2347    33606 Graptolithina    33534 Hemichordata     33518
    ## 2362    33606 Graptolithina    33534 Hemichordata     33518
    ## 2368    33606 Graptolithina    33534 Hemichordata     33518
    ## 2376    33606 Graptolithina    33534 Hemichordata     33518
    ## 2379    33606 Graptolithina    33534 Hemichordata     33518
    ## 2399    33606 Graptolithina    33534 Hemichordata     33518
    ## 2400    33606 Graptolithina    33534 Hemichordata     33518
    ## 2413    33606 Graptolithina    33534 Hemichordata     33518
    ## 2424    33606 Graptolithina    33534 Hemichordata     33518
    ## 2425    33606 Graptolithina    33534 Hemichordata     33518
    ## 2437    33606 Graptolithina    33534 Hemichordata     33518
    ## 2456    33606 Graptolithina    33534 Hemichordata     33518
    ## 2459    33606 Graptolithina    33534 Hemichordata     33518
    ## 2463    33606 Graptolithina    33534 Hemichordata     33518
    ## 2464    33606 Graptolithina    33534 Hemichordata     33518
    ## 2466    33606 Graptolithina    33534 Hemichordata     33518
    ## 2501    33606 Graptolithina    33534 Hemichordata     33518
    ## 2502    33606 Graptolithina    33534 Hemichordata     33518
    ## 2505    33606 Graptolithina    33534 Hemichordata     33518
    ## 2507    33606 Graptolithina    33534 Hemichordata     33518
    ## 2508    33606 Graptolithina    33534 Hemichordata     33518
    ## 2518    33606 Graptolithina    33534 Hemichordata     33518
    ## 2520    33606 Graptolithina    33534 Hemichordata     33518
    ## 2521    33606 Graptolithina    33534 Hemichordata     33518
    ## 2525    33606 Graptolithina    33534 Hemichordata     33518
    ## 2526    33606 Graptolithina    33534 Hemichordata     33518
    ## 2527    33606 Graptolithina    33534 Hemichordata     33518
    ## 2528    33606 Graptolithina    33534 Hemichordata     33518
    ## 2530    33606 Graptolithina    33534 Hemichordata     33518
    ## 2562    33606 Graptolithina    33534 Hemichordata     33518
    ## 2565    33606 Graptolithina    33534 Hemichordata     33518
    ## 2585    33606 Graptolithina    33534 Hemichordata     33518
    ## 2587    33606 Graptolithina    33534 Hemichordata     33518
    ## 2593    33606 Graptolithina    33534 Hemichordata     33518
    ## 2644    33606 Graptolithina    33534 Hemichordata     33518
    ## 2646    33606 Graptolithina    33534 Hemichordata     33518
    ## 2661    33606 Graptolithina    33534 Hemichordata     33518
    ## 2706    33606 Graptolithina    33534 Hemichordata     33518
    ## 2707    33606 Graptolithina    33534 Hemichordata     33518
    ## 2708    33606 Graptolithina    33534 Hemichordata     33518
    ## 2710    33606 Graptolithina    33534 Hemichordata     33518
    ## 2755    33606 Graptolithina    33534 Hemichordata     33518
    ## 2793    33606 Graptolithina    33534 Hemichordata     33518
    ## 2797    33606 Graptolithina    33534 Hemichordata     33518
    ## 2798    33606 Graptolithina    33534 Hemichordata     33518
    ## 2799    33606 Graptolithina    33534 Hemichordata     33518
    ## 2804    33606 Graptolithina    33534 Hemichordata     33518
    ## 2806    33606 Graptolithina    33534 Hemichordata     33518
    ## 2807    33606 Graptolithina    33534 Hemichordata     33518
    ## 2809    33606 Graptolithina    33534 Hemichordata     33518
    ## 2810    33606 Graptolithina    33534 Hemichordata     33518
    ## 2884    33606 Graptolithina    33534 Hemichordata     33518
    ## 2891    33606 Graptolithina    33534 Hemichordata     33518
    ## 2892    33606 Graptolithina    33534 Hemichordata     33518
    ## 2893    33606 Graptolithina    33534 Hemichordata     33518
    ## 2934    33606 Graptolithina    33534 Hemichordata     33518
    ## 2935    33606 Graptolithina    33534 Hemichordata     33518
    ## 2943    33606 Graptolithina    33534 Hemichordata     33518
    ## 2948    33606 Graptolithina    33534 Hemichordata     33518
    ## 3021    33606 Graptolithina    33534 Hemichordata     33518
    ## 3108    33606 Graptolithina    33534 Hemichordata     33518
    ## 3110    33606 Graptolithina    33534 Hemichordata     33518
    ## 3116    33606 Graptolithina    33534 Hemichordata     33518
    ## 3127    33606 Graptolithina    33534 Hemichordata     33518
    ## 3128    33606 Graptolithina    33534 Hemichordata     33518
    ## 3129    33606 Graptolithina    33534 Hemichordata     33518
    ## 3148    33606 Graptolithina    33534 Hemichordata     33518
    ## 3149    33606 Graptolithina    33534 Hemichordata     33518
    ## 3173    33606 Graptolithina    33534 Hemichordata     33518
    ## 3182    33606 Graptolithina    33534 Hemichordata     33518
    ## 3199    33606 Graptolithina    33534 Hemichordata     33518
    ## 3200    33606 Graptolithina    33534 Hemichordata     33518
    ## 3202    33606 Graptolithina    33534 Hemichordata     33518
    ## 3246    33606 Graptolithina    33534 Hemichordata     33518
    ## 3248    33606 Graptolithina    33534 Hemichordata     33518
    ## 3276    33606 Graptolithina    33534 Hemichordata     33518
    ## 3290    33606 Graptolithina    33534 Hemichordata     33518
    ## 3318    33606 Graptolithina    33534 Hemichordata     33518
    ## 3353    33606 Graptolithina    33534 Hemichordata     33518
    ## 3358    33606 Graptolithina    33534 Hemichordata     33518
    ## 3366    33606 Graptolithina    33534 Hemichordata     33518
    ## 3377    33606 Graptolithina    33534 Hemichordata     33518
    ## 3386    33606 Graptolithina    33534 Hemichordata     33518
    ## 3403    33606 Graptolithina    33534 Hemichordata     33518
    ## 3462    33606 Graptolithina    33534 Hemichordata     33518
    ## 3473    33606 Graptolithina    33534 Hemichordata     33518
    ## 3479    33606 Graptolithina    33534 Hemichordata     33518
    ## 3485    33606 Graptolithina    33534 Hemichordata     33518
    ## 3530    33606 Graptolithina    33534 Hemichordata     33518
    ## 3541    33606 Graptolithina    33534 Hemichordata     33518
    ## 3545    33606 Graptolithina    33534 Hemichordata     33518
    ## 3677    33606 Graptolithina    33534 Hemichordata     33518
    ## 3842    33606 Graptolithina    33534 Hemichordata     33518
    ## 3847    33606 Graptolithina    33534 Hemichordata     33518
    ## 3848    33606 Graptolithina    33534 Hemichordata     33518
    ## 3849    33606 Graptolithina    33534 Hemichordata     33518
    ## 3857    33606 Graptolithina    33534 Hemichordata     33518
    ## 3859    33606 Graptolithina    33534 Hemichordata     33518
    ## 3866    33606 Graptolithina    33534 Hemichordata     33518
    ## 3867    33606 Graptolithina    33534 Hemichordata     33518
    ## 3894    33606 Graptolithina    33534 Hemichordata     33518
    ## 3903    33606 Graptolithina    33534 Hemichordata     33518
    ## 3912    33606 Graptolithina    33534 Hemichordata     33518
    ## 3919    33606 Graptolithina    33534 Hemichordata     33518
    ## 3937    33606 Graptolithina    33534 Hemichordata     33518
    ## 3941    33606 Graptolithina    33534 Hemichordata     33518
    ## 3942    33606 Graptolithina    33534 Hemichordata     33518
    ## 3949    33606 Graptolithina    33534 Hemichordata     33518
    ## 3956    33606 Graptolithina    33534 Hemichordata     33518
    ## 3968    33606 Graptolithina    33534 Hemichordata     33518
    ## 3979    33606 Graptolithina    33534 Hemichordata     33518
    ## 3983    33606 Graptolithina    33534 Hemichordata     33518
    ## 3998    33606 Graptolithina    33534 Hemichordata     33518
    ## 4011    33606 Graptolithina    33534 Hemichordata     33518
    ## 4023    33606 Graptolithina    33534 Hemichordata     33518
    ## 4038    33606 Graptolithina    33534 Hemichordata     33518
    ## 4041    33606 Graptolithina    33534 Hemichordata     33518
    ## 4046    33606 Graptolithina    33534 Hemichordata     33518
    ## 4051    33606 Graptolithina    33534 Hemichordata     33518
    ## 4061    33606 Graptolithina    33534 Hemichordata     33518
    ## 4062    33606 Graptolithina    33534 Hemichordata     33518
    ## 4067    33606 Graptolithina    33534 Hemichordata     33518
    ## 4072    33606 Graptolithina    33534 Hemichordata     33518
    ## 4075    33606 Graptolithina    33534 Hemichordata     33518
    ## 4096    33606 Graptolithina    33534 Hemichordata     33518
    ## 4097    33606 Graptolithina    33534 Hemichordata     33518
    ## 4099    33606 Graptolithina    33534 Hemichordata     33518
    ## 4101    33606 Graptolithina    33534 Hemichordata     33518
    ## 4102    33606 Graptolithina    33534 Hemichordata     33518
    ## 4104    33606 Graptolithina    33534 Hemichordata     33518
    ## 4110    33606 Graptolithina    33534 Hemichordata     33518
    ## 4113    33606 Graptolithina    33534 Hemichordata     33518
    ## 4115    33606 Graptolithina    33534 Hemichordata     33518
    ## 4138    33606 Graptolithina    33534 Hemichordata     33518
    ## 4141    33606 Graptolithina    33534 Hemichordata     33518
    ## 4142    33606 Graptolithina    33534 Hemichordata     33518
    ## 4150    33606 Graptolithina    33534 Hemichordata     33518
    ## 4166    33606 Graptolithina    33534 Hemichordata     33518
    ## 4167    33606 Graptolithina    33534 Hemichordata     33518
    ## 4256    33606 Graptolithina    33534 Hemichordata     33518
    ## 4257    33606 Graptolithina    33534 Hemichordata     33518
    ## 4266    33606 Graptolithina    33534 Hemichordata     33518
    ## 4267    33606 Graptolithina    33534 Hemichordata     33518
    ## 4286    33606 Graptolithina    33534 Hemichordata     33518
    ## 4292    33606 Graptolithina    33534 Hemichordata     33518
    ## 4293    33606 Graptolithina    33534 Hemichordata     33518
    ## 4302    33606 Graptolithina    33534 Hemichordata     33518
    ## 4303    33606 Graptolithina    33534 Hemichordata     33518
    ## 4305    33606 Graptolithina    33534 Hemichordata     33518
    ## 4309    33606 Graptolithina    33534 Hemichordata     33518
    ## 4316    33606 Graptolithina    33534 Hemichordata     33518
    ## 4317    33606 Graptolithina    33534 Hemichordata     33518
    ## 4320    33606 Graptolithina    33534 Hemichordata     33518
    ## 4325    33606 Graptolithina    33534 Hemichordata     33518
    ## 4332    33606 Graptolithina    33534 Hemichordata     33518
    ## 4333    33606 Graptolithina    33534 Hemichordata     33518
    ## 4340    33606 Graptolithina    33534 Hemichordata     33518
    ## 4345    33606 Graptolithina    33534 Hemichordata     33518
    ## 4350    33606 Graptolithina    33534 Hemichordata     33518
    ## 4353    33606 Graptolithina    33534 Hemichordata     33518
    ## 4354    33606 Graptolithina    33534 Hemichordata     33518
    ## 4355    33606 Graptolithina    33534 Hemichordata     33518
    ## 4358    33606 Graptolithina    33534 Hemichordata     33518
    ## 4366    33606 Graptolithina    33534 Hemichordata     33518
    ## 4379    33606 Graptolithina    33534 Hemichordata     33518
    ## 4386    33606 Graptolithina    33534 Hemichordata     33518
    ## 4391    33606 Graptolithina    33534 Hemichordata     33518
    ## 4402    33606 Graptolithina    33534 Hemichordata     33518
    ## 4413    33606 Graptolithina    33534 Hemichordata     33518
    ## 4414    33606 Graptolithina    33534 Hemichordata     33518
    ## 4436    33606 Graptolithina    33534 Hemichordata     33518
    ## 4444    33606 Graptolithina    33534 Hemichordata     33518
    ## 4498    33606 Graptolithina    33534 Hemichordata     33518
    ## 4501    33606 Graptolithina    33534 Hemichordata     33518
    ## 4516    33606 Graptolithina    33534 Hemichordata     33518
    ## 4522    33606 Graptolithina    33534 Hemichordata     33518
    ## 4662    33606 Graptolithina    33534 Hemichordata     33518
    ## 4667    33606 Graptolithina    33534 Hemichordata     33518
    ## 4671    33606 Graptolithina    33534 Hemichordata     33518
    ## 4673    33606 Graptolithina    33534 Hemichordata     33518
    ## 4685    33606 Graptolithina    33534 Hemichordata     33518
    ## 4686    33606 Graptolithina    33534 Hemichordata     33518
    ## 4695    33606 Graptolithina    33534 Hemichordata     33518
    ## 4703    33606 Graptolithina    33534 Hemichordata     33518
    ## 4713    33606 Graptolithina    33534 Hemichordata     33518
    ## 4725    33606 Graptolithina    33534 Hemichordata     33518
    ## 4726    33606 Graptolithina    33534 Hemichordata     33518
    ## 4748    33606 Graptolithina    33534 Hemichordata     33518
    ## 4756    33606 Graptolithina    33534 Hemichordata     33518
    ## 4765    33606 Graptolithina    33534 Hemichordata     33518
    ## 4773    33606 Graptolithina    33534 Hemichordata     33518
    ## 4774    33606 Graptolithina    33534 Hemichordata     33518
    ## 4775    33606 Graptolithina    33534 Hemichordata     33518
    ## 4776    33606 Graptolithina    33534 Hemichordata     33518
    ## 4777    33606 Graptolithina    33534 Hemichordata     33518
    ## 4780    33606 Graptolithina    33534 Hemichordata     33518
    ## 4781    33606 Graptolithina    33534 Hemichordata     33518
    ## 4782    33606 Graptolithina    33534 Hemichordata     33518
    ## 4816    33606 Graptolithina    33534 Hemichordata     33518
    ## 4817    33606 Graptolithina    33534 Hemichordata     33518
    ## 4818    33606 Graptolithina    33534 Hemichordata     33518
    ## 4819    33606 Graptolithina    33534 Hemichordata     33518
    ## 4820    33606 Graptolithina    33534 Hemichordata     33518
    ## 4821    33606 Graptolithina    33534 Hemichordata     33518
    ## 4822    33606 Graptolithina    33534 Hemichordata     33518
    ## 4823    33606 Graptolithina    33534 Hemichordata     33518
    ## 4824    33606 Graptolithina    33534 Hemichordata     33518
    ## 4825    33606 Graptolithina    33534 Hemichordata     33518
    ## 4826    33606 Graptolithina    33534 Hemichordata     33518
    ## 4827    33606 Graptolithina    33534 Hemichordata     33518
    ## 4828    33606 Graptolithina    33534 Hemichordata     33518
    ## 4829    33606 Graptolithina    33534 Hemichordata     33518
    ## 4830    33606 Graptolithina    33534 Hemichordata     33518
    ## 4831    33606 Graptolithina    33534 Hemichordata     33518
    ## 4833    33606 Graptolithina    33534 Hemichordata     33518
    ## 4834    33606 Graptolithina    33534 Hemichordata     33518
    ## 4835    33606 Graptolithina    33534 Hemichordata     33518
    ## 4836    33606 Graptolithina    33534 Hemichordata     33518
    ## 4837    33606 Graptolithina    33534 Hemichordata     33518
    ## 4838    33606 Graptolithina    33534 Hemichordata     33518
    ## 4839    33606 Graptolithina    33534 Hemichordata     33518
    ## 4883    33606 Graptolithina    33534 Hemichordata     33518
    ## 4884    33606 Graptolithina    33534 Hemichordata     33518
    ## 4885    33606 Graptolithina    33534 Hemichordata     33518
    ## 4886    33606 Graptolithina    33534 Hemichordata     33518
    ## 4887    33606 Graptolithina    33534 Hemichordata     33518
    ## 4888    33606 Graptolithina    33534 Hemichordata     33518
    ## 4889    33606 Graptolithina    33534 Hemichordata     33518
    ## 4890    33606 Graptolithina    33534 Hemichordata     33518
    ## 4891    33606 Graptolithina    33534 Hemichordata     33518
    ## 4892    33606 Graptolithina    33534 Hemichordata     33518
    ## 4893    33606 Graptolithina    33534 Hemichordata     33518
    ## 4899    33606 Graptolithina    33534 Hemichordata     33518
    ## 4900    33606 Graptolithina    33534 Hemichordata     33518
    ## 4901    33606 Graptolithina    33534 Hemichordata     33518
    ## 4902    33606 Graptolithina    33534 Hemichordata     33518
    ## 4903    33606 Graptolithina    33534 Hemichordata     33518
    ## 4904    33606 Graptolithina    33534 Hemichordata     33518
    ## 4905    33606 Graptolithina    33534 Hemichordata     33518
    ## 4906    33606 Graptolithina    33534 Hemichordata     33518
    ## 4907    33606 Graptolithina    33534 Hemichordata     33518
    ## 4908    33606 Graptolithina    33534 Hemichordata     33518
    ## 4909    33606 Graptolithina    33534 Hemichordata     33518
    ## 4910    33606 Graptolithina    33534 Hemichordata     33518
    ## 4911    33606 Graptolithina    33534 Hemichordata     33518
    ## 4912    33606 Graptolithina    33534 Hemichordata     33518
    ## 4913    33606 Graptolithina    33534 Hemichordata     33518
    ## 4914    33606 Graptolithina    33534 Hemichordata     33518
    ## 4915    33606 Graptolithina    33534 Hemichordata     33518
    ## 4916    33606 Graptolithina    33534 Hemichordata     33518
    ## 4917    33606 Graptolithina    33534 Hemichordata     33518
    ## 4918    33606 Graptolithina    33534 Hemichordata     33518
    ## 4919    33606 Graptolithina    33534 Hemichordata     33518
    ## 4920    33606 Graptolithina    33534 Hemichordata     33518
    ## 4921    33606 Graptolithina    33534 Hemichordata     33518
    ## 4923    33606 Graptolithina    33534 Hemichordata     33518
    ## 4924    33606 Graptolithina    33534 Hemichordata     33518
    ## 4925    33606 Graptolithina    33534 Hemichordata     33518
    ## 4926    33606 Graptolithina    33534 Hemichordata     33518
    ## 4927    33606 Graptolithina    33534 Hemichordata     33518
    ## 4928    33606 Graptolithina    33534 Hemichordata     33518
    ## 4929    33606 Graptolithina    33534 Hemichordata     33518
    ## 4962    33606 Graptolithina    33534 Hemichordata     33518
    ## 4963    33606 Graptolithina    33534 Hemichordata     33518
    ## 4964    33606 Graptolithina    33534 Hemichordata     33518
    ## 5102    33606 Graptolithina    33534 Hemichordata     33518
    ## 5103    33606 Graptolithina    33534 Hemichordata     33518
    ## 5106    33606 Graptolithina    33534 Hemichordata     33518
    ## 5110    33606 Graptolithina    33534 Hemichordata     33518
    ## 5114    33606 Graptolithina    33534 Hemichordata     33518
    ## 5115    33606 Graptolithina    33534 Hemichordata     33518
    ## 5126    33606 Graptolithina    33534 Hemichordata     33518
    ## 5127    33606 Graptolithina    33534 Hemichordata     33518
    ## 5128    33606 Graptolithina    33534 Hemichordata     33518
    ## 5129    33606 Graptolithina    33534 Hemichordata     33518
    ## 5130    33606 Graptolithina    33534 Hemichordata     33518
    ## 5131    33606 Graptolithina    33534 Hemichordata     33518
    ## 5132    33606 Graptolithina    33534 Hemichordata     33518
    ## 5150    33606 Graptolithina    33534 Hemichordata     33518
    ## 5151    33606 Graptolithina    33534 Hemichordata     33518
    ## 5152    33606 Graptolithina    33534 Hemichordata     33518
    ## 5153    33606 Graptolithina    33534 Hemichordata     33518
    ## 5154    33606 Graptolithina    33534 Hemichordata     33518
    ## 5155    33606 Graptolithina    33534 Hemichordata     33518
    ## 5167    33606 Graptolithina    33534 Hemichordata     33518
    ## 5176    33606 Graptolithina    33534 Hemichordata     33518
    ## 5177    33606 Graptolithina    33534 Hemichordata     33518
    ## 5195    33606 Graptolithina    33534 Hemichordata     33518
    ## 5204    33606 Graptolithina    33534 Hemichordata     33518
    ## 5205    33606 Graptolithina    33534 Hemichordata     33518
    ## 5248    33606 Graptolithina    33534 Hemichordata     33518
    ## 5249    33606 Graptolithina    33534 Hemichordata     33518
    ## 5250    33606 Graptolithina    33534 Hemichordata     33518
    ## 5251    33606 Graptolithina    33534 Hemichordata     33518
    ## 5253    33606 Graptolithina    33534 Hemichordata     33518
    ## 5256    33606 Graptolithina    33534 Hemichordata     33518
    ## 5260    33606 Graptolithina    33534 Hemichordata     33518
    ## 5261    33606 Graptolithina    33534 Hemichordata     33518
    ## 5262    33606 Graptolithina    33534 Hemichordata     33518
    ## 5263    33606 Graptolithina    33534 Hemichordata     33518
    ## 5265    33606 Graptolithina    33534 Hemichordata     33518
    ## 5268    33606 Graptolithina    33534 Hemichordata     33518
    ## 5270    33606 Graptolithina    33534 Hemichordata     33518
    ## 5275    33606 Graptolithina    33534 Hemichordata     33518
    ## 5277    33606 Graptolithina    33534 Hemichordata     33518
    ## 5281    33606 Graptolithina    33534 Hemichordata     33518
    ## 5286    33606 Graptolithina    33534 Hemichordata     33518
    ## 5287    33606 Graptolithina    33534 Hemichordata     33518
    ## 5289    33606 Graptolithina    33534 Hemichordata     33518
    ## 5293    33606 Graptolithina    33534 Hemichordata     33518
    ## 5298    33606 Graptolithina    33534 Hemichordata     33518
    ## 5299    33606 Graptolithina    33534 Hemichordata     33518
    ## 5300    33606 Graptolithina    33534 Hemichordata     33518
    ## 5301    33606 Graptolithina    33534 Hemichordata     33518
    ## 5302    33606 Graptolithina    33534 Hemichordata     33518
    ## 5305    33606 Graptolithina    33534 Hemichordata     33518
    ## 5306    33606 Graptolithina    33534 Hemichordata     33518
    ## 5307    33606 Graptolithina    33534 Hemichordata     33518
    ## 5314    33606 Graptolithina    33534 Hemichordata     33518
    ## 5315    33606 Graptolithina    33534 Hemichordata     33518
    ## 5319    33606 Graptolithina    33534 Hemichordata     33518
    ## 5320    33606 Graptolithina    33534 Hemichordata     33518
    ## 5322    33606 Graptolithina    33534 Hemichordata     33518
    ## 5323    33606 Graptolithina    33534 Hemichordata     33518
    ## 5326    33606 Graptolithina    33534 Hemichordata     33518
    ## 5327    33606 Graptolithina    33534 Hemichordata     33518
    ## 5330    33606 Graptolithina    33534 Hemichordata     33518
    ## 5333    33606 Graptolithina    33534 Hemichordata     33518
    ## 5342    33606 Graptolithina    33534 Hemichordata     33518
    ## 5343    33606 Graptolithina    33534 Hemichordata     33518
    ## 5344    33606 Graptolithina    33534 Hemichordata     33518
    ## 5345    33606 Graptolithina    33534 Hemichordata     33518
    ## 5346    33606 Graptolithina    33534 Hemichordata     33518
    ## 5347    33606 Graptolithina    33534 Hemichordata     33518
    ## 5353    33606 Graptolithina    33534 Hemichordata     33518
    ## 5354    33606 Graptolithina    33534 Hemichordata     33518
    ## 5355    33606 Graptolithina    33534 Hemichordata     33518
    ## 5363    33606 Graptolithina    33534 Hemichordata     33518
    ## 5364    33606 Graptolithina    33534 Hemichordata     33518
    ## 5365    33606 Graptolithina    33534 Hemichordata     33518
    ## 5385    33606 Graptolithina    33534 Hemichordata     33518
    ## 5486    33606 Graptolithina    33534 Hemichordata     33518
    ## 5487    33606 Graptolithina    33534 Hemichordata     33518
    ## 5488    33606 Graptolithina    33534 Hemichordata     33518
    ## 5490    33606 Graptolithina    33534 Hemichordata     33518
    ## 5495    33606 Graptolithina    33534 Hemichordata     33518
    ## 5496    33606 Graptolithina    33534 Hemichordata     33518
    ## 5506    33606 Graptolithina    33534 Hemichordata     33518
    ## 5508    33606 Graptolithina    33534 Hemichordata     33518
    ## 5513    33606 Graptolithina    33534 Hemichordata     33518
    ## 5515    33606 Graptolithina    33534 Hemichordata     33518
    ## 5518    33606 Graptolithina    33534 Hemichordata     33518
    ## 5523    33606 Graptolithina    33534 Hemichordata     33518
    ## 5524    33606 Graptolithina    33534 Hemichordata     33518
    ## 5525    33606 Graptolithina    33534 Hemichordata     33518
    ## 5530    33606 Graptolithina    33534 Hemichordata     33518
    ## 5532    33606 Graptolithina    33534 Hemichordata     33518
    ## 5538    33606 Graptolithina    33534 Hemichordata     33518
    ## 5544    33606 Graptolithina    33534 Hemichordata     33518
    ## 5547    33606 Graptolithina    33534 Hemichordata     33518
    ## 5548    33606 Graptolithina    33534 Hemichordata     33518
    ## 5549    33606 Graptolithina    33534 Hemichordata     33518
    ## 5554    33606 Graptolithina    33534 Hemichordata     33518
    ## 5559    33606 Graptolithina    33534 Hemichordata     33518
    ## 5563    33606 Graptolithina    33534 Hemichordata     33518
    ## 5565    33606 Graptolithina    33534 Hemichordata     33518
    ## 5567    33606 Graptolithina    33534 Hemichordata     33518
    ## 5568    33606 Graptolithina    33534 Hemichordata     33518
    ## 5573    33606 Graptolithina    33534 Hemichordata     33518
    ## 5575    33606 Graptolithina    33534 Hemichordata     33518
    ## 5585    33606 Graptolithina    33534 Hemichordata     33518
    ## 5586    33606 Graptolithina    33534 Hemichordata     33518
    ## 5587    33606 Graptolithina    33534 Hemichordata     33518
    ## 5588    33606 Graptolithina    33534 Hemichordata     33518
    ## 5593    33606 Graptolithina    33534 Hemichordata     33518
    ## 5598    33606 Graptolithina    33534 Hemichordata     33518
    ## 5599    33606 Graptolithina    33534 Hemichordata     33518
    ## 5602    33606 Graptolithina    33534 Hemichordata     33518
    ## 5606    33606 Graptolithina    33534 Hemichordata     33518
    ## 5607    33606 Graptolithina    33534 Hemichordata     33518
    ## 5610    33606 Graptolithina    33534 Hemichordata     33518
    ## 5611    33606 Graptolithina    33534 Hemichordata     33518
    ## 5613    33606 Graptolithina    33534 Hemichordata     33518
    ## 5616    33606 Graptolithina    33534 Hemichordata     33518
    ## 5617    33606 Graptolithina    33534 Hemichordata     33518
    ## 5621    33606 Graptolithina    33534 Hemichordata     33518
    ## 5625    33606 Graptolithina    33534 Hemichordata     33518
    ## 5631    33606 Graptolithina    33534 Hemichordata     33518
    ## 5632    33606 Graptolithina    33534 Hemichordata     33518
    ## 5633    33606 Graptolithina    33534 Hemichordata     33518
    ## 5637    33606 Graptolithina    33534 Hemichordata     33518
    ## 5641    33606 Graptolithina    33534 Hemichordata     33518
    ## 5646    33606 Graptolithina    33534 Hemichordata     33518
    ## 5670    33606 Graptolithina    33534 Hemichordata     33518
    ## 5673    33606 Graptolithina    33534 Hemichordata     33518
    ## 5719    33606 Graptolithina    33534 Hemichordata     33518
    ## 5724    33606 Graptolithina    33534 Hemichordata     33518
    ## 5726    33606 Graptolithina    33534 Hemichordata     33518
    ## 5727    33606 Graptolithina    33534 Hemichordata     33518
    ## 5731    33606 Graptolithina    33534 Hemichordata     33518
    ## 5732    33606 Graptolithina    33534 Hemichordata     33518
    ## 5735    33606 Graptolithina    33534 Hemichordata     33518
    ## 5740    33606 Graptolithina    33534 Hemichordata     33518
    ## 5742    33606 Graptolithina    33534 Hemichordata     33518
    ## 5743    33606 Graptolithina    33534 Hemichordata     33518
    ## 5745    33606 Graptolithina    33534 Hemichordata     33518
    ## 5747    33606 Graptolithina    33534 Hemichordata     33518
    ## 5748    33606 Graptolithina    33534 Hemichordata     33518
    ## 5752    33606 Graptolithina    33534 Hemichordata     33518
    ## 5754    33606 Graptolithina    33534 Hemichordata     33518
    ## 5760    33606 Graptolithina    33534 Hemichordata     33518
    ## 5764    33606 Graptolithina    33534 Hemichordata     33518
    ## 5766    33606 Graptolithina    33534 Hemichordata     33518
    ## 5776    33606 Graptolithina    33534 Hemichordata     33518
    ## 5783    33606 Graptolithina    33534 Hemichordata     33518
    ## 5843    33606 Graptolithina    33534 Hemichordata     33518
    ## 5845    33606 Graptolithina    33534 Hemichordata     33518
    ## 5871    33606 Graptolithina    33534 Hemichordata     33518
    ## 5886    33606 Graptolithina    33534 Hemichordata     33518
    ## 5892    33606 Graptolithina    33534 Hemichordata     33518
    ## 5896    33606 Graptolithina    33534 Hemichordata     33518
    ##                authorizer              enterer             modifier
    ## 32           Sepkoski, J.          Sommers, M.              unknown
    ## 39           Sepkoski, J.          Sommers, M.              unknown
    ## 56           Sepkoski, J.          Sommers, M.              unknown
    ## 58           Sepkoski, J.          Sommers, M.              unknown
    ## 66           Sepkoski, J.          Sommers, M.              unknown
    ## 74           Sepkoski, J.          Sommers, M.              unknown
    ## 77           Sepkoski, J.          Sommers, M.              unknown
    ## 83           Sepkoski, J.          Sommers, M.           Wagner, P.
    ## 89           Sepkoski, J.          Sommers, M.              unknown
    ## 94           Sepkoski, J.          Sommers, M.              unknown
    ## 105          Sepkoski, J.          Sommers, M.              unknown
    ## 110          Sepkoski, J.          Sommers, M.              unknown
    ## 115          Sepkoski, J.          Sommers, M.              unknown
    ## 117          Sepkoski, J.          Sommers, M.              unknown
    ## 120          Sepkoski, J.          Sommers, M.              unknown
    ## 122          Sepkoski, J.          Sommers, M.              unknown
    ## 128          Sepkoski, J.          Sommers, M.              unknown
    ## 131          Sepkoski, J.          Sommers, M.              unknown
    ## 152          Sepkoski, J.          Sommers, M.           Wagner, P.
    ## 156          Sepkoski, J.          Sommers, M.              unknown
    ## 181          Sepkoski, J.          Sommers, M.              unknown
    ## 192          Sepkoski, J.          Sommers, M.              unknown
    ## 194          Sepkoski, J.          Sommers, M.              unknown
    ## 214            Miller, A. Novack-Gottshall, P.           Wagner, P.
    ## 226            Miller, A. Novack-Gottshall, P.              unknown
    ## 233             Alroy, J.          Sommers, M.              unknown
    ## 234             Alroy, J.          Sommers, M.              unknown
    ## 236             Alroy, J.          Sommers, M.              unknown
    ## 237             Alroy, J.          Sommers, M.              unknown
    ## 257            Miller, A. Novack-Gottshall, P.              unknown
    ## 259            Miller, A. Novack-Gottshall, P.              unknown
    ## 261            Miller, A. Novack-Gottshall, P.              unknown
    ## 264            Miller, A. Novack-Gottshall, P.              unknown
    ## 267            Miller, A. Novack-Gottshall, P.              unknown
    ## 269            Miller, A. Novack-Gottshall, P.              unknown
    ## 273            Miller, A. Novack-Gottshall, P.              unknown
    ## 276            Miller, A. Novack-Gottshall, P.              unknown
    ## 283            Miller, A. Novack-Gottshall, P.              unknown
    ## 294            Miller, A. Novack-Gottshall, P.              unknown
    ## 298            Miller, A. Novack-Gottshall, P.              unknown
    ## 303            Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 312            Miller, A. Novack-Gottshall, P.              unknown
    ## 400            Miller, A. Novack-Gottshall, P.              unknown
    ## 411            Miller, A. Novack-Gottshall, P.              unknown
    ## 415            Miller, A. Novack-Gottshall, P.              unknown
    ## 416            Miller, A. Novack-Gottshall, P.              unknown
    ## 418            Miller, A. Novack-Gottshall, P.           Wagner, P.
    ## 422            Miller, A. Novack-Gottshall, P.              unknown
    ## 436             Alroy, J.          Sommers, M.          Sommers, M.
    ## 444            Miller, A. Novack-Gottshall, P.              unknown
    ## 472            Miller, A. Novack-Gottshall, P.              unknown
    ## 482            Miller, A. Novack-Gottshall, P.              unknown
    ## 489            Miller, A. Novack-Gottshall, P.              unknown
    ## 493            Miller, A. Novack-Gottshall, P.              unknown
    ## 502            Miller, A. Novack-Gottshall, P.              unknown
    ## 511            Miller, A. Novack-Gottshall, P.              unknown
    ## 523            Miller, A. Novack-Gottshall, P.              unknown
    ## 529            Miller, A. Novack-Gottshall, P.              unknown
    ## 534            Miller, A. Novack-Gottshall, P.              unknown
    ## 544            Miller, A. Novack-Gottshall, P.              unknown
    ## 549            Miller, A. Novack-Gottshall, P.              unknown
    ## 553            Miller, A. Novack-Gottshall, P.              unknown
    ## 560            Miller, A. Novack-Gottshall, P.              unknown
    ## 571            Miller, A. Novack-Gottshall, P.              unknown
    ## 579            Miller, A. Novack-Gottshall, P.              unknown
    ## 586            Miller, A. Novack-Gottshall, P.              unknown
    ## 587            Miller, A. Novack-Gottshall, P.              unknown
    ## 627            Miller, A. Novack-Gottshall, P.              unknown
    ## 634            Miller, A. Novack-Gottshall, P.              unknown
    ## 641            Miller, A. Novack-Gottshall, P.              unknown
    ## 659            Miller, A. Novack-Gottshall, P.              unknown
    ## 665            Miller, A. Novack-Gottshall, P.              unknown
    ## 666            Miller, A. Novack-Gottshall, P.              unknown
    ## 670            Miller, A. Novack-Gottshall, P.              unknown
    ## 698            Miller, A. Novack-Gottshall, P.              unknown
    ## 706            Miller, A. Novack-Gottshall, P.              unknown
    ## 725            Miller, A. Novack-Gottshall, P.              unknown
    ## 729            Miller, A. Novack-Gottshall, P.              unknown
    ## 734            Miller, A. Novack-Gottshall, P.              unknown
    ## 738            Miller, A. Novack-Gottshall, P.              unknown
    ## 741            Miller, A. Novack-Gottshall, P.              unknown
    ## 746            Miller, A. Novack-Gottshall, P.              unknown
    ## 759            Miller, A. Novack-Gottshall, P.              unknown
    ## 791            Miller, A. Novack-Gottshall, P.              unknown
    ## 795            Miller, A. Novack-Gottshall, P.              unknown
    ## 808            Miller, A. Novack-Gottshall, P.              unknown
    ## 813            Miller, A. Novack-Gottshall, P.              unknown
    ## 819            Miller, A. Novack-Gottshall, P.              unknown
    ## 837            Miller, A. Novack-Gottshall, P.              unknown
    ## 865            Miller, A. Novack-Gottshall, P.              unknown
    ## 887            Miller, A. Novack-Gottshall, P.              unknown
    ## 891            Miller, A. Novack-Gottshall, P.              unknown
    ## 918            Miller, A. Novack-Gottshall, P.              unknown
    ## 920            Miller, A. Novack-Gottshall, P.              unknown
    ## 923            Miller, A. Novack-Gottshall, P.              unknown
    ## 929            Miller, A. Novack-Gottshall, P.              unknown
    ## 933            Miller, A. Novack-Gottshall, P.              unknown
    ## 949            Miller, A. Novack-Gottshall, P.              unknown
    ## 960            Miller, A. Novack-Gottshall, P.              unknown
    ## 968            Miller, A. Novack-Gottshall, P.              unknown
    ## 1000           Miller, A. Novack-Gottshall, P.              unknown
    ## 1003           Miller, A. Novack-Gottshall, P.              unknown
    ## 1012           Miller, A. Novack-Gottshall, P.              unknown
    ## 1016           Miller, A. Novack-Gottshall, P.              unknown
    ## 1027           Miller, A. Novack-Gottshall, P.              unknown
    ## 1059           Miller, A. Novack-Gottshall, P.              unknown
    ## 1086           Miller, A. Novack-Gottshall, P.              unknown
    ## 1090           Miller, A. Novack-Gottshall, P.              unknown
    ## 1101           Miller, A. Novack-Gottshall, P.              unknown
    ## 1130           Miller, A. Novack-Gottshall, P.              unknown
    ## 1138           Miller, A. Novack-Gottshall, P.              unknown
    ## 1163           Miller, A. Novack-Gottshall, P.              unknown
    ## 1166           Miller, A. Novack-Gottshall, P.              unknown
    ## 1213           Miller, A. Novack-Gottshall, P.              unknown
    ## 1215           Miller, A. Novack-Gottshall, P.              unknown
    ## 1221           Miller, A. Novack-Gottshall, P.              unknown
    ## 1229           Miller, A. Novack-Gottshall, P.              unknown
    ## 1247           Miller, A. Novack-Gottshall, P.              unknown
    ## 1252           Miller, A. Novack-Gottshall, P.              unknown
    ## 1273           Miller, A. Novack-Gottshall, P.              unknown
    ## 1285           Miller, A. Novack-Gottshall, P.              unknown
    ## 1290           Miller, A. Novack-Gottshall, P.              unknown
    ## 1305           Miller, A. Novack-Gottshall, P.              unknown
    ## 1309           Miller, A. Novack-Gottshall, P.              unknown
    ## 1315            Alroy, J.          Sommers, M.              unknown
    ## 1316            Alroy, J.          Sommers, M.              unknown
    ## 1317            Alroy, J.          Sommers, M.              unknown
    ## 1360           Miller, A. Novack-Gottshall, P.              unknown
    ## 1394           Miller, A. Novack-Gottshall, P.              unknown
    ## 1412           Miller, A. Novack-Gottshall, P.              unknown
    ## 1416           Miller, A. Novack-Gottshall, P.              unknown
    ## 1432           Miller, A. Novack-Gottshall, P.              unknown
    ## 1465           Miller, A. Novack-Gottshall, P.              unknown
    ## 1473           Miller, A. Novack-Gottshall, P.              unknown
    ## 1554       Patzkowsky, M.             Krug, Z.              unknown
    ## 1556       Patzkowsky, M.             Krug, Z.              unknown
    ## 1566       Patzkowsky, M.             Krug, Z.              unknown
    ## 1568       Patzkowsky, M.             Krug, Z.              unknown
    ## 1569            Foote, M.         Koverman, K.           Wagner, P.
    ## 1571            Foote, M.         Koverman, K.           Wagner, P.
    ## 1573          Holland, S.           Hanson, T.              unknown
    ## 1574          Holland, S.           Hanson, T.              unknown
    ## 1575          Holland, S.           Hanson, T.              unknown
    ## 1579          Holland, S.           Hanson, T.              unknown
    ## 1580          Holland, S.           Hanson, T.              unknown
    ## 1581          Holland, S.           Hanson, T.              unknown
    ## 1582          Holland, S.           Hanson, T.              unknown
    ## 1586          Holland, S.           Hanson, T.              unknown
    ## 1590            Foote, M.            Foote, M.              unknown
    ## 1591            Foote, M.            Foote, M.              unknown
    ## 1596            Foote, M.            Foote, M.              unknown
    ## 1597            Foote, M.            Foote, M.              unknown
    ## 1599            Foote, M.            Foote, M.              unknown
    ## 1600            Foote, M.            Foote, M.              unknown
    ## 1601            Foote, M.            Foote, M.              unknown
    ## 1605            Foote, M.            Foote, M.              unknown
    ## 1606            Foote, M.            Foote, M.              unknown
    ## 1612            Foote, M.            Foote, M.              unknown
    ## 1613            Foote, M.            Foote, M.              unknown
    ## 1637            Foote, M.            Foote, M.              unknown
    ## 1648            Foote, M.            Foote, M.              unknown
    ## 1839            Foote, M.            Foote, M.              unknown
    ## 2120           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2124           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2128           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2140           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2150           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2166           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2173           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2185           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2192           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2199           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2202           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2211           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2214           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2224           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2234           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2239           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2246           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2256           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2291           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2317           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2325           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2328           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2341           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2347           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2362           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2368           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2376           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2379           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2399          Holland, S.           Hanson, T.              unknown
    ## 2400          Holland, S.           Hanson, T.              unknown
    ## 2413          Holland, S.           Hanson, T.              unknown
    ## 2424          Holland, S.           Hanson, T.              unknown
    ## 2425          Holland, S.           Hanson, T.              unknown
    ## 2437          Holland, S.           Hanson, T.              unknown
    ## 2456          Holland, S.           Hanson, T.              unknown
    ## 2459          Holland, S.           Hanson, T.              unknown
    ## 2463          Holland, S.           Hanson, T.              unknown
    ## 2464          Holland, S.           Hanson, T.              unknown
    ## 2466          Holland, S.           Hanson, T.              unknown
    ## 2501            Foote, M.            Foote, M.              unknown
    ## 2502            Foote, M.            Foote, M.              unknown
    ## 2505            Foote, M.            Foote, M.              unknown
    ## 2507          Holland, S.           Hanson, T.              unknown
    ## 2508          Holland, S.           Hanson, T.              unknown
    ## 2518          Holland, S.           Hanson, T.              unknown
    ## 2520          Holland, S.           Hanson, T.              unknown
    ## 2521          Holland, S.           Hanson, T.              unknown
    ## 2525          Holland, S.           Hanson, T.              unknown
    ## 2526          Holland, S.           Hanson, T.              unknown
    ## 2527          Holland, S.           Hanson, T.              unknown
    ## 2528          Holland, S.           Hanson, T.              unknown
    ## 2530          Holland, S.           Hanson, T.              unknown
    ## 2562          Holland, S.           Hanson, T.              unknown
    ## 2565          Holland, S.           Hanson, T.              unknown
    ## 2585          Holland, S.           Hanson, T.              unknown
    ## 2587          Holland, S.           Hanson, T.              unknown
    ## 2593          Holland, S.           Hanson, T.              unknown
    ## 2644           Miller, A. Novack-Gottshall, P.           Miller, A.
    ## 2646           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2661           Miller, A. Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2706            Foote, M.            Foote, M.              unknown
    ## 2707            Foote, M.            Foote, M.              unknown
    ## 2708            Foote, M.            Foote, M.              unknown
    ## 2710            Foote, M.            Foote, M.              unknown
    ## 2755            Foote, M.            Foote, M.              unknown
    ## 2793          Holland, S.           Hanson, T.              unknown
    ## 2797          Holland, S.           Hanson, T.              unknown
    ## 2798          Holland, S.           Hanson, T.              unknown
    ## 2799          Holland, S.           Hanson, T.              unknown
    ## 2804          Holland, S.           Hanson, T.              unknown
    ## 2806          Holland, S.           Hanson, T.              unknown
    ## 2807          Holland, S.           Hanson, T.              unknown
    ## 2809          Holland, S.           Hanson, T.           Wagner, P.
    ## 2810          Holland, S.           Hanson, T.           Wagner, P.
    ## 2884            Foote, M.            Foote, M.              unknown
    ## 2891            Foote, M.            Foote, M.              unknown
    ## 2892            Foote, M.            Foote, M.              unknown
    ## 2893            Foote, M.            Foote, M.              unknown
    ## 2934            Foote, M.            Foote, M.              unknown
    ## 2935            Foote, M.            Foote, M.              unknown
    ## 2943            Foote, M.            Foote, M.              unknown
    ## 2948            Foote, M.            Foote, M.              unknown
    ## 3021            Foote, M.            Foote, M.              unknown
    ## 3108            Foote, M.            Foote, M.              unknown
    ## 3110            Foote, M.            Foote, M.              unknown
    ## 3116            Foote, M.            Foote, M.              unknown
    ## 3127            Foote, M.            Foote, M.              unknown
    ## 3128            Foote, M.            Foote, M.              unknown
    ## 3129            Foote, M.            Foote, M.              unknown
    ## 3148            Foote, M.            Foote, M.              unknown
    ## 3149            Foote, M.            Foote, M.              unknown
    ## 3173            Foote, M.            Foote, M.              unknown
    ## 3182            Foote, M.            Foote, M.              unknown
    ## 3199            Foote, M.            Foote, M.              unknown
    ## 3200            Foote, M.            Foote, M.              unknown
    ## 3202            Foote, M.            Foote, M.              unknown
    ## 3246            Foote, M.            Foote, M.              unknown
    ## 3248            Foote, M.            Foote, M.              unknown
    ## 3276            Foote, M.            Foote, M.              unknown
    ## 3290            Foote, M.            Foote, M.              unknown
    ## 3318            Foote, M.            Foote, M.              unknown
    ## 3353            Foote, M.            Foote, M.            Foote, M.
    ## 3358            Foote, M.            Foote, M.              unknown
    ## 3366            Foote, M.            Foote, M.              unknown
    ## 3377            Foote, M.            Foote, M.              unknown
    ## 3386            Foote, M.            Foote, M.              unknown
    ## 3403          Holland, S.          Holland, S.           Wagner, P.
    ## 3462           Wagner, P.         Koverman, K.              unknown
    ## 3473           Miller, A. Novack-Gottshall, P.              unknown
    ## 3479           Miller, A. Novack-Gottshall, P.              unknown
    ## 3485           Miller, A. Novack-Gottshall, P.              unknown
    ## 3530          Aberhan, M.         Nurnberg, S.              unknown
    ## 3541       Patzkowsky, M.             Krug, Z.              unknown
    ## 3545       Patzkowsky, M.             Krug, Z.              unknown
    ## 3677            Hendy, A.            Hendy, A.              unknown
    ## 3842            Hendy, A.            Hendy, A.              unknown
    ## 3847            Hendy, A.            Hendy, A.              unknown
    ## 3848            Hendy, A.            Hendy, A.              unknown
    ## 3849            Hendy, A.            Hendy, A.              unknown
    ## 3857            Hendy, A.            Hendy, A.              unknown
    ## 3859            Hendy, A.            Hendy, A.              unknown
    ## 3866            Hendy, A.            Hendy, A.            Hendy, A.
    ## 3867            Hendy, A.            Hendy, A.            Hendy, A.
    ## 3894            Hendy, A.            Hendy, A.            Hendy, A.
    ## 3903            Hendy, A.            Hendy, A.              unknown
    ## 3912            Hendy, A.            Hendy, A.              unknown
    ## 3919            Hendy, A.            Hendy, A.              unknown
    ## 3937            Hendy, A.            Hendy, A.              unknown
    ## 3941            Hendy, A.            Hendy, A.              unknown
    ## 3942            Hendy, A.            Hendy, A.              unknown
    ## 3949            Hendy, A.            Hendy, A.              unknown
    ## 3956            Hendy, A.            Hendy, A.              unknown
    ## 3968            Hendy, A.            Hendy, A.              unknown
    ## 3979            Hendy, A.            Hendy, A.              unknown
    ## 3983            Hendy, A.            Hendy, A.              unknown
    ## 3998            Hendy, A.            Hendy, A.              unknown
    ## 4011            Hendy, A.            Hendy, A.              unknown
    ## 4023          Holland, S.          Holland, S.              unknown
    ## 4038        Kiessling, W.           Merkel, U.              unknown
    ## 4041 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4046 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4051 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4061 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4062 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4067 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4072 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4075 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4096            Ivany, L.             Wall, P.              unknown
    ## 4097            Ivany, L.             Wall, P.              unknown
    ## 4099            Ivany, L.             Wall, P.              unknown
    ## 4101            Ivany, L.             Wall, P.              unknown
    ## 4102            Ivany, L.             Wall, P.              unknown
    ## 4104 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4110 Novack-Gottshall, P.            Hearn, P. Novack-Gottshall, P.
    ## 4113 Novack-Gottshall, P.            Hearn, P. Novack-Gottshall, P.
    ## 4115 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4138 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4141 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4142 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4150 Novack-Gottshall, P.            Hearn, P.              unknown
    ## 4166 Novack-Gottshall, P.            Hearn, P.           Wagner, P.
    ## 4167 Novack-Gottshall, P.            Hearn, P.           Wagner, P.
    ## 4256          Hopkins, M.          Hopkins, M.              unknown
    ## 4257          Hopkins, M.          Hopkins, M.              unknown
    ## 4266          Hopkins, M.          Hopkins, M.              unknown
    ## 4267          Hopkins, M.          Hopkins, M.              unknown
    ## 4286          Hopkins, M.          Hopkins, M.              unknown
    ## 4292         Finnegan, S.         Finnegan, S.              unknown
    ## 4293         Finnegan, S.         Finnegan, S.              unknown
    ## 4302           Miller, A.            Kolbe, S.            Kolbe, S.
    ## 4303           Miller, A.            Kolbe, S.              unknown
    ## 4305           Miller, A.            Kolbe, S.              unknown
    ## 4309           Miller, A.            Kolbe, S.              unknown
    ## 4316           Miller, A.            Kolbe, S.            Kolbe, S.
    ## 4317           Miller, A.            Kolbe, S.              unknown
    ## 4320           Miller, A.            Kolbe, S.            Kolbe, S.
    ## 4325           Miller, A.            Kolbe, S.              unknown
    ## 4332           Miller, A.            Kolbe, S.              unknown
    ## 4333           Miller, A.            Kolbe, S.              unknown
    ## 4340           Miller, A.            Kolbe, S.              unknown
    ## 4345           Miller, A.            Kolbe, S.              unknown
    ## 4350           Miller, A.            Kolbe, S.              unknown
    ## 4353           Miller, A.            Kolbe, S.              unknown
    ## 4354           Miller, A.            Kolbe, S.              unknown
    ## 4355           Miller, A.            Kolbe, S.              unknown
    ## 4358           Miller, A.            Kolbe, S.              unknown
    ## 4366           Miller, A.            Kolbe, S.              unknown
    ## 4379           Miller, A.            Kolbe, S.              unknown
    ## 4386           Miller, A.            Kolbe, S.              unknown
    ## 4391           Miller, A.            Kolbe, S.              unknown
    ## 4402           Miller, A.            Kolbe, S.              unknown
    ## 4413           Miller, A.            Kolbe, S.              unknown
    ## 4414           Miller, A.            Kolbe, S.              unknown
    ## 4436           Miller, A.            Kolbe, S.              unknown
    ## 4444           Miller, A.            Kolbe, S.              unknown
    ## 4498           Miller, A.            Kolbe, S.              unknown
    ## 4501           Miller, A.            Kolbe, S.              unknown
    ## 4516        Kiessling, W.           Merkel, U.              unknown
    ## 4522        Kiessling, W.           Merkel, U.              unknown
    ## 4662        Kiessling, W.           Krause, M.              unknown
    ## 4667        Kiessling, W.           Krause, M.              unknown
    ## 4671        Kiessling, W.           Krause, M.              unknown
    ## 4673        Kiessling, W.           Krause, M.              unknown
    ## 4685        Kiessling, W.           Krause, M.              unknown
    ## 4686        Kiessling, W.           Krause, M.              unknown
    ## 4695        Kiessling, W.           Krause, M.           Krause, M.
    ## 4703        Kiessling, W.           Krause, M.              unknown
    ## 4713        Kiessling, W.           Krause, M.              unknown
    ## 4725        Kiessling, W.           Krause, M.              unknown
    ## 4726        Kiessling, W.           Krause, M.              unknown
    ## 4748        Kiessling, W.           Krause, M.              unknown
    ## 4756        Kiessling, W.           Krause, M.              unknown
    ## 4765        Kiessling, W.           Krause, M.              unknown
    ## 4773        Kiessling, W.           Krause, M.           Krause, M.
    ## 4774        Kiessling, W.           Krause, M.           Krause, M.
    ## 4775        Kiessling, W.           Krause, M.           Krause, M.
    ## 4776        Kiessling, W.           Krause, M.           Krause, M.
    ## 4777        Kiessling, W.           Krause, M.           Krause, M.
    ## 4780        Kiessling, W.           Krause, M.           Krause, M.
    ## 4781        Kiessling, W.           Krause, M.              unknown
    ## 4782        Kiessling, W.           Krause, M.           Krause, M.
    ## 4816        Kiessling, W.           Krause, M.           Krause, M.
    ## 4817        Kiessling, W.           Krause, M.           Krause, M.
    ## 4818        Kiessling, W.           Krause, M.           Krause, M.
    ## 4819        Kiessling, W.           Krause, M.           Krause, M.
    ## 4820        Kiessling, W.           Krause, M.           Krause, M.
    ## 4821        Kiessling, W.           Krause, M.           Krause, M.
    ## 4822        Kiessling, W.           Krause, M.           Krause, M.
    ## 4823        Kiessling, W.           Krause, M.           Krause, M.
    ## 4824        Kiessling, W.           Krause, M.           Krause, M.
    ## 4825        Kiessling, W.           Krause, M.           Krause, M.
    ## 4826        Kiessling, W.           Krause, M.           Krause, M.
    ## 4827        Kiessling, W.           Krause, M.           Krause, M.
    ## 4828        Kiessling, W.           Krause, M.           Krause, M.
    ## 4829        Kiessling, W.           Krause, M.           Krause, M.
    ## 4830        Kiessling, W.           Krause, M.           Krause, M.
    ## 4831        Kiessling, W.           Krause, M.           Krause, M.
    ## 4833        Kiessling, W.           Krause, M.           Krause, M.
    ## 4834        Kiessling, W.           Krause, M.           Krause, M.
    ## 4835        Kiessling, W.           Krause, M.           Krause, M.
    ## 4836        Kiessling, W.           Krause, M.           Krause, M.
    ## 4837        Kiessling, W.           Krause, M.           Krause, M.
    ## 4838        Kiessling, W.           Krause, M.           Krause, M.
    ## 4839        Kiessling, W.           Krause, M.           Krause, M.
    ## 4883        Kiessling, W.           Krause, M.           Krause, M.
    ## 4884        Kiessling, W.           Krause, M.           Krause, M.
    ## 4885        Kiessling, W.           Krause, M.           Krause, M.
    ## 4886        Kiessling, W.           Krause, M.           Krause, M.
    ## 4887        Kiessling, W.           Krause, M.           Krause, M.
    ## 4888        Kiessling, W.           Krause, M.           Krause, M.
    ## 4889        Kiessling, W.           Krause, M.           Krause, M.
    ## 4890        Kiessling, W.           Krause, M.           Krause, M.
    ## 4891        Kiessling, W.           Krause, M.           Krause, M.
    ## 4892        Kiessling, W.           Krause, M.           Krause, M.
    ## 4893        Kiessling, W.           Krause, M.           Krause, M.
    ## 4899        Kiessling, W.           Krause, M.           Krause, M.
    ## 4900        Kiessling, W.           Krause, M.           Krause, M.
    ## 4901        Kiessling, W.           Krause, M.           Krause, M.
    ## 4902        Kiessling, W.           Krause, M.           Krause, M.
    ## 4903        Kiessling, W.           Krause, M.           Krause, M.
    ## 4904        Kiessling, W.           Krause, M.           Krause, M.
    ## 4905        Kiessling, W.           Krause, M.           Krause, M.
    ## 4906        Kiessling, W.           Krause, M.           Krause, M.
    ## 4907        Kiessling, W.           Krause, M.           Krause, M.
    ## 4908        Kiessling, W.           Krause, M.           Krause, M.
    ## 4909        Kiessling, W.           Krause, M.           Krause, M.
    ## 4910        Kiessling, W.           Krause, M.           Krause, M.
    ## 4911        Kiessling, W.           Krause, M.           Krause, M.
    ## 4912        Kiessling, W.           Krause, M.           Krause, M.
    ## 4913        Kiessling, W.           Krause, M.           Krause, M.
    ## 4914        Kiessling, W.           Krause, M.           Krause, M.
    ## 4915        Kiessling, W.           Krause, M.           Krause, M.
    ## 4916        Kiessling, W.           Krause, M.           Krause, M.
    ## 4917        Kiessling, W.           Krause, M.           Krause, M.
    ## 4918        Kiessling, W.           Krause, M.           Krause, M.
    ## 4919        Kiessling, W.           Krause, M.           Krause, M.
    ## 4920        Kiessling, W.           Krause, M.           Krause, M.
    ## 4921        Kiessling, W.           Krause, M.           Krause, M.
    ## 4923        Kiessling, W.           Krause, M.           Krause, M.
    ## 4924        Kiessling, W.           Krause, M.           Krause, M.
    ## 4925        Kiessling, W.           Krause, M.           Krause, M.
    ## 4926        Kiessling, W.           Krause, M.           Krause, M.
    ## 4927        Kiessling, W.           Krause, M.           Krause, M.
    ## 4928        Kiessling, W.           Krause, M.           Krause, M.
    ## 4929        Kiessling, W.           Krause, M.           Krause, M.
    ## 4962        Kiessling, W.           Krause, M.           Krause, M.
    ## 4963        Kiessling, W.           Krause, M.           Krause, M.
    ## 4964        Kiessling, W.           Krause, M.           Krause, M.
    ## 5102        Kiessling, W.           Krause, M.              unknown
    ## 5103        Kiessling, W.           Krause, M.              unknown
    ## 5106        Kiessling, W.           Krause, M.              unknown
    ## 5110        Kiessling, W.           Krause, M.              unknown
    ## 5114        Kiessling, W.           Krause, M.              unknown
    ## 5115        Kiessling, W.           Krause, M.              unknown
    ## 5126        Kiessling, W.           Krause, M.              unknown
    ## 5127        Kiessling, W.           Krause, M.              unknown
    ## 5128        Kiessling, W.           Krause, M.              unknown
    ## 5129        Kiessling, W.           Krause, M.              unknown
    ## 5130        Kiessling, W.           Krause, M.              unknown
    ## 5131        Kiessling, W.           Krause, M.              unknown
    ## 5132        Kiessling, W.           Krause, M.              unknown
    ## 5150        Kiessling, W.           Krause, M.              unknown
    ## 5151        Kiessling, W.           Krause, M.              unknown
    ## 5152        Kiessling, W.           Krause, M.              unknown
    ## 5153        Kiessling, W.           Krause, M.              unknown
    ## 5154        Kiessling, W.           Krause, M.              unknown
    ## 5155        Kiessling, W.           Krause, M.              unknown
    ## 5167        Kiessling, W.           Krause, M.              unknown
    ## 5176        Kiessling, W.           Krause, M.              unknown
    ## 5177        Kiessling, W.           Krause, M.              unknown
    ## 5195        Kiessling, W.           Krause, M.              unknown
    ## 5204        Kiessling, W.           Krause, M.              unknown
    ## 5205        Kiessling, W.           Krause, M.              unknown
    ## 5248        Kiessling, W.           Krause, M.              unknown
    ## 5249        Kiessling, W.           Krause, M.              unknown
    ## 5250        Kiessling, W.           Krause, M.              unknown
    ## 5251        Kiessling, W.           Krause, M.              unknown
    ## 5253        Kiessling, W.           Krause, M.              unknown
    ## 5256        Kiessling, W.           Krause, M.              unknown
    ## 5260        Kiessling, W.           Krause, M.              unknown
    ## 5261        Kiessling, W.           Krause, M.              unknown
    ## 5262        Kiessling, W.           Krause, M.              unknown
    ## 5263        Kiessling, W.           Krause, M.              unknown
    ## 5265        Kiessling, W.           Krause, M.              unknown
    ## 5268        Kiessling, W.           Krause, M.              unknown
    ## 5270        Kiessling, W.           Krause, M.              unknown
    ## 5275        Kiessling, W.           Krause, M.              unknown
    ## 5277        Kiessling, W.           Krause, M.              unknown
    ## 5281        Kiessling, W.           Krause, M.              unknown
    ## 5286        Kiessling, W.           Krause, M.              unknown
    ## 5287        Kiessling, W.           Krause, M.              unknown
    ## 5289        Kiessling, W.           Krause, M.              unknown
    ## 5293        Kiessling, W.           Krause, M.              unknown
    ## 5298        Kiessling, W.           Krause, M.              unknown
    ## 5299        Kiessling, W.           Krause, M.              unknown
    ## 5300        Kiessling, W.           Krause, M.              unknown
    ## 5301        Kiessling, W.           Krause, M.              unknown
    ## 5302        Kiessling, W.           Krause, M.              unknown
    ## 5305        Kiessling, W.           Krause, M.              unknown
    ## 5306        Kiessling, W.           Krause, M.              unknown
    ## 5307        Kiessling, W.           Krause, M.              unknown
    ## 5314        Kiessling, W.           Krause, M.              unknown
    ## 5315        Kiessling, W.           Krause, M.              unknown
    ## 5319        Kiessling, W.           Krause, M.              unknown
    ## 5320        Kiessling, W.           Krause, M.              unknown
    ## 5322        Kiessling, W.           Krause, M.              unknown
    ## 5323        Kiessling, W.           Krause, M.              unknown
    ## 5326        Kiessling, W.           Krause, M.              unknown
    ## 5327        Kiessling, W.           Krause, M.              unknown
    ## 5330        Kiessling, W.           Krause, M.              unknown
    ## 5333        Kiessling, W.           Krause, M.              unknown
    ## 5342        Kiessling, W.           Krause, M.              unknown
    ## 5343        Kiessling, W.           Krause, M.              unknown
    ## 5344        Kiessling, W.           Krause, M.              unknown
    ## 5345        Kiessling, W.           Krause, M.              unknown
    ## 5346        Kiessling, W.           Krause, M.              unknown
    ## 5347        Kiessling, W.           Krause, M.              unknown
    ## 5353        Kiessling, W.           Krause, M.              unknown
    ## 5354        Kiessling, W.           Krause, M.              unknown
    ## 5355        Kiessling, W.           Krause, M.              unknown
    ## 5363        Kiessling, W.           Krause, M.           Krause, M.
    ## 5364        Kiessling, W.           Krause, M.           Krause, M.
    ## 5365        Kiessling, W.           Krause, M.           Krause, M.
    ## 5385        Kiessling, W.           Krause, M.           Krause, M.
    ## 5486        Kiessling, W.           Krause, M.              unknown
    ## 5487        Kiessling, W.           Krause, M.              unknown
    ## 5488        Kiessling, W.           Krause, M.              unknown
    ## 5490        Kiessling, W.           Krause, M.              unknown
    ## 5495        Kiessling, W.           Krause, M.              unknown
    ## 5496        Kiessling, W.           Krause, M.              unknown
    ## 5506        Kiessling, W.           Krause, M.              unknown
    ## 5508        Kiessling, W.           Krause, M.              unknown
    ## 5513        Kiessling, W.           Krause, M.              unknown
    ## 5515        Kiessling, W.           Krause, M.              unknown
    ## 5518        Kiessling, W.           Krause, M.              unknown
    ## 5523        Kiessling, W.           Krause, M.              unknown
    ## 5524        Kiessling, W.           Krause, M.              unknown
    ## 5525        Kiessling, W.           Krause, M.              unknown
    ## 5530        Kiessling, W.           Krause, M.              unknown
    ## 5532        Kiessling, W.           Krause, M.              unknown
    ## 5538        Kiessling, W.           Krause, M.              unknown
    ## 5544        Kiessling, W.           Krause, M.              unknown
    ## 5547        Kiessling, W.           Krause, M.              unknown
    ## 5548        Kiessling, W.           Krause, M.              unknown
    ## 5549        Kiessling, W.           Krause, M.              unknown
    ## 5554        Kiessling, W.           Krause, M.              unknown
    ## 5559        Kiessling, W.           Krause, M.              unknown
    ## 5563        Kiessling, W.           Krause, M.              unknown
    ## 5565        Kiessling, W.           Krause, M.              unknown
    ## 5567        Kiessling, W.           Krause, M.              unknown
    ## 5568        Kiessling, W.           Krause, M.              unknown
    ## 5573        Kiessling, W.           Krause, M.              unknown
    ## 5575        Kiessling, W.           Krause, M.              unknown
    ## 5585        Kiessling, W.           Krause, M.              unknown
    ## 5586        Kiessling, W.           Krause, M.              unknown
    ## 5587        Kiessling, W.           Krause, M.              unknown
    ## 5588        Kiessling, W.           Krause, M.              unknown
    ## 5593        Kiessling, W.           Krause, M.              unknown
    ## 5598        Kiessling, W.           Krause, M.              unknown
    ## 5599        Kiessling, W.           Krause, M.              unknown
    ## 5602        Kiessling, W.           Krause, M.              unknown
    ## 5606        Kiessling, W.           Krause, M.              unknown
    ## 5607        Kiessling, W.           Krause, M.              unknown
    ## 5610        Kiessling, W.           Krause, M.              unknown
    ## 5611        Kiessling, W.           Krause, M.              unknown
    ## 5613        Kiessling, W.           Krause, M.              unknown
    ## 5616        Kiessling, W.           Krause, M.              unknown
    ## 5617        Kiessling, W.           Krause, M.              unknown
    ## 5621        Kiessling, W.           Krause, M.              unknown
    ## 5625        Kiessling, W.           Krause, M.              unknown
    ## 5631        Kiessling, W.           Krause, M.              unknown
    ## 5632        Kiessling, W.           Krause, M.              unknown
    ## 5633        Kiessling, W.           Krause, M.              unknown
    ## 5637        Kiessling, W.           Krause, M.              unknown
    ## 5641        Kiessling, W.           Krause, M.              unknown
    ## 5646        Kiessling, W.           Krause, M.              unknown
    ## 5670        Kiessling, W.           Krause, M.              unknown
    ## 5673        Kiessling, W.           Krause, M.              unknown
    ## 5719        Kiessling, W.           Krause, M.              unknown
    ## 5724        Kiessling, W.           Krause, M.              unknown
    ## 5726        Kiessling, W.           Krause, M.              unknown
    ## 5727        Kiessling, W.           Krause, M.              unknown
    ## 5731        Kiessling, W.           Krause, M.              unknown
    ## 5732        Kiessling, W.           Krause, M.              unknown
    ## 5735        Kiessling, W.           Krause, M.              unknown
    ## 5740        Kiessling, W.           Krause, M.              unknown
    ## 5742        Kiessling, W.           Krause, M.              unknown
    ## 5743        Kiessling, W.           Krause, M.              unknown
    ## 5745        Kiessling, W.           Krause, M.              unknown
    ## 5747        Kiessling, W.           Krause, M.              unknown
    ## 5748        Kiessling, W.           Krause, M.              unknown
    ## 5752        Kiessling, W.           Krause, M.              unknown
    ## 5754        Kiessling, W.           Krause, M.              unknown
    ## 5760        Kiessling, W.           Krause, M.              unknown
    ## 5764        Kiessling, W.           Krause, M.              unknown
    ## 5766        Kiessling, W.           Krause, M.              unknown
    ## 5776        Kiessling, W.           Krause, M.              unknown
    ## 5783        Kiessling, W.           Krause, M.              unknown
    ## 5843           Wagner, P.           Wagner, P.              unknown
    ## 5845           Wagner, P.           Wagner, P.              unknown
    ## 5871           Kroger, B.           Kroger, B.              unknown
    ## 5886           Wagner, P.           Wagner, P.              unknown
    ## 5892           Wagner, P.           Wagner, P.              unknown
    ## 5896           Wagner, P.           Wagner, P.              unknown
    ## 
    ## $Monograptidae
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 33            2764  occurrence      NA       NA           297
    ## 49            2843  occurrence      NA       NA           303
    ## 51            2945  occurrence      NA       NA           309
    ## 62            3394  occurrence      NA       NA           328
    ## 80            3792  occurrence      NA       NA           339
    ## 165           7377  occurrence      NA       NA           515
    ## 197           9370  occurrence      NA       NA           436
    ## 211          36011  occurrence      NA       NA          2655
    ## 225          37591  occurrence      NA       NA          2866
    ## 230          38205  occurrence      NA       NA          2709
    ## 238          42759  occurrence      NA       NA          3340
    ## 241          42762  occurrence      NA       NA          3341
    ## 245          42790  occurrence      NA       NA          3345
    ## 255          48402  occurrence      NA       NA          2761
    ## 278          48874  occurrence      NA       NA          2931
    ## 285          48932  occurrence      NA       NA          2933
    ## 289          48999  occurrence      NA       NA          2939
    ## 295          49213  occurrence      NA       NA          2946
    ## 307          49373  occurrence      NA       NA          2950
    ## 316          49394  occurrence      NA       NA          3179
    ## 325          49427  occurrence      NA       NA          3181
    ## 333          49435  occurrence      NA       NA          3182
    ## 360          49752  occurrence      NA       NA          3255
    ## 408          51774  occurrence      NA       NA          3859
    ## 413          51955  occurrence      NA       NA          3863
    ## 417          52063  occurrence      NA       NA          3865
    ## 424          52252  occurrence      NA       NA          3875
    ## 426          52324  occurrence      NA       NA          3879
    ## 427          52356  occurrence      NA       NA          3880
    ## 428          52379  occurrence      NA       NA          3882
    ## 440          93752  occurrence      NA       NA          6986
    ## 448         105286  occurrence      NA       NA          2951
    ## 476         105405  occurrence      NA       NA          4665
    ## 484         105413  occurrence      NA       NA          4666
    ## 492         105421  occurrence      NA       NA          4667
    ## 498         105427  occurrence      NA       NA          4668
    ## 513         105461  occurrence      NA       NA          4674
    ## 531         105480  occurrence      NA       NA          4677
    ## 536         105485  occurrence      NA       NA          4678
    ## 548         105515  occurrence      NA       NA          4682
    ## 550         105517  occurrence      NA       NA          4683
    ## 552         105525  occurrence      NA       NA          4684
    ## 556         105545  occurrence      NA       NA          4685
    ## 584         105733  occurrence      NA       NA          4709
    ## 592         105803  occurrence      NA       NA          4711
    ## 597         105946  occurrence      NA       NA          4715
    ## 636         106419  occurrence      NA       NA          4748
    ## 645         106463  occurrence      NA       NA          4755
    ## 647         106484  occurrence      NA       NA          4757
    ## 673         106638  occurrence      NA       NA          5136
    ## 676         106652  occurrence      NA       NA          5141
    ## 679         106673  occurrence      NA       NA          5251
    ## 695         106729  occurrence      NA       NA          5267
    ## 700         106797  occurrence      NA       NA          5337
    ## 707         106833  occurrence      NA       NA          5405
    ## 726         106938  occurrence      NA       NA          5427
    ## 749         107025  occurrence      NA       NA          7263
    ## 752         107040  occurrence      NA       NA          7265
    ## 779         107176  occurrence      NA       NA          7359
    ## 800         107256  occurrence      NA       NA          7384
    ## 815         107314  occurrence      NA       NA          7639
    ## 817         107320  occurrence      NA       NA          7640
    ## 829         107350  occurrence      NA       NA          7646
    ## 844         107422  occurrence      NA       NA          7659
    ## 845         107426  occurrence      NA       NA          7660
    ## 859         107488  occurrence      NA       NA          7669
    ## 867         107522  occurrence      NA       NA          7677
    ## 895         107654  occurrence      NA       NA          7699
    ## 905         107669  occurrence      NA       NA          7700
    ## 939         107733  occurrence      NA       NA          7710
    ## 951         107748  occurrence      NA       NA          7713
    ## 970         107866  occurrence      NA       NA          7725
    ## 979         107886  occurrence      NA       NA          7727
    ## 1005        108047  occurrence      NA       NA          7748
    ## 1015        108072  occurrence      NA       NA          7751
    ## 1022        108079  occurrence      NA       NA          7753
    ## 1038        108096  occurrence      NA       NA          7756
    ## 1045        108103  occurrence      NA       NA          7757
    ## 1061        108142  occurrence      NA       NA          7761
    ## 1073        108154  occurrence      NA       NA          7763
    ## 1096        108252  occurrence      NA       NA          7770
    ## 1111        108268  occurrence      NA       NA          7772
    ## 1144        108390  occurrence      NA       NA          7782
    ## 1153        108399  occurrence      NA       NA          7783
    ## 1178        108429  occurrence      NA       NA          7796
    ## 1184        108435  occurrence      NA       NA          7798
    ## 1188        108439  occurrence      NA       NA          7800
    ## 1195        108446  occurrence      NA       NA          7801
    ## 1202        108473  occurrence      NA       NA          7805
    ## 1207        108479  occurrence      NA       NA          7806
    ## 1239        108539  occurrence      NA       NA          7814
    ## 1256        108592  occurrence      NA       NA          7834
    ## 1262        108651  occurrence      NA       NA          7839
    ## 1275        108749  occurrence      NA       NA          7847
    ## 1294        108915  occurrence      NA       NA          7885
    ## 1297        108944  occurrence      NA       NA          7886
    ## 1329        118181  occurrence      NA       NA          8776
    ## 1341        118308  occurrence      NA       NA          8800
    ## 1365        118506  occurrence      NA       NA          8858
    ## 1388        118624  occurrence      NA       NA          8871
    ## 1409        118722  occurrence      NA       NA          8885
    ## 1418        118731  occurrence      NA       NA          8887
    ## 1426        118743  occurrence      NA       NA          8888
    ## 1438        118787  occurrence      NA       NA          8891
    ## 1443        118795  occurrence      NA       NA          8892
    ## 1474        118980  occurrence      NA       NA          9036
    ## 1476        118997  occurrence      NA       NA          9039
    ## 1594        154401  occurrence      NA       NA         13704
    ## 1607        154414  occurrence      NA       NA         13707
    ## 1614        154421  occurrence      NA       NA         13708
    ## 1664        154471  occurrence      NA       NA         13711
    ## 2131        240581  occurrence      NA       NA          8529
    ## 2145        240649  occurrence      NA       NA          8534
    ## 2154        240658  occurrence      NA       NA          8535
    ## 2163        240691  occurrence      NA       NA          8538
    ## 2167        240813  occurrence      NA       NA          8549
    ## 2178        240851  occurrence      NA       NA          8552
    ## 2187        240887  occurrence      NA       NA          8557
    ## 2193        240898  occurrence      NA       NA          8558
    ## 2197        240910  occurrence      NA       NA          8560
    ## 2217        240985  occurrence      NA       NA          8565
    ## 2236        241047  occurrence      NA       NA          8569
    ## 2242        241066  occurrence      NA       NA          8571
    ## 2249        241073  occurrence      NA       NA          8572
    ## 2259        241096  occurrence      NA       NA          8575
    ## 2287        242114  occurrence      NA       NA         20764
    ## 2340        242428  occurrence      NA       NA         20803
    ## 2343        242433  occurrence      NA       NA         20804
    ## 2355        242450  occurrence      NA       NA         20805
    ## 2360        242489  occurrence      NA       NA         20808
    ## 2367        242514  occurrence      NA       NA         20810
    ## 2370        242517  occurrence      NA       NA         23582
    ## 2382        242546  occurrence      NA       NA         23593
    ## 2415        251717  occurrence      NA       NA         24520
    ## 2417        251847  occurrence      NA       NA         24537
    ## 2427        254216  occurrence      NA       NA         24606
    ## 2428        254217  occurrence      NA       NA         24606
    ## 2429        254218  occurrence      NA       NA         24607
    ## 2445        254572  occurrence      NA       NA         24719
    ## 2452        255076  occurrence      NA       NA         24750
    ## 2454        255090  occurrence      NA       NA         24756
    ## 2489        256744  occurrence      NA       NA         24908
    ## 2499        259303  occurrence      NA       NA         25072
    ## 2513        259694  occurrence      NA       NA         25106
    ## 2515        259696  occurrence      NA       NA         25107
    ## 2516        259697  occurrence      NA       NA         25111
    ## 2517        259712  occurrence      NA       NA         25109
    ## 2529        260373  occurrence      NA       NA         25167
    ## 2538        260382  occurrence      NA       NA         25170
    ## 2615        263807  occurrence      NA       NA         25533
    ## 2648        264692  occurrence      NA       NA         20893
    ## 2655        264774  occurrence      NA       NA         20898
    ## 2662        264964  occurrence      NA       NA         20932
    ## 2687        265517  occurrence      NA       NA         21012
    ## 2690        265556  occurrence      NA       NA         21017
    ## 2831        281551  occurrence      NA       NA         26816
    ## 2882        285887  occurrence      NA       NA         27180
    ## 2936        286769  occurrence      NA       NA         27337
    ## 2937        286770  occurrence      NA       NA         27337
    ## 3028        287572  occurrence      NA       NA         27456
    ## 3102        290605  occurrence      NA       NA         27736
    ## 3106        290627  occurrence      NA       NA         27739
    ## 3115        290639  occurrence      NA       NA         27741
    ## 3125        290860  occurrence      NA       NA         27765
    ## 3201        291408  occurrence      NA       NA         27798
    ## 3215        291426  occurrence      NA       NA         27799
    ## 3234        292204  occurrence      NA       NA         27813
    ## 3235        292205  occurrence      NA       NA         27813
    ## 3275        292475  occurrence      NA       NA         27849
    ## 3301        292688  occurrence      NA       NA         27860
    ## 3305        292695  occurrence      NA       NA         27862
    ## 3306        292696  occurrence      NA       NA         27862
    ## 3363        292951  occurrence      NA       NA         27902
    ## 3364        292952  occurrence      NA       NA         27902
    ## 3378        293067  occurrence      NA       NA         27910
    ## 3456        435025  occurrence      NA       NA         42516
    ## 3457        435026  occurrence      NA       NA         42517
    ## 3470        446190  occurrence      NA       NA          8680
    ## 3477        446214  occurrence      NA       NA          8681
    ## 3487        446265  occurrence      NA       NA          8686
    ## 3506        446298  occurrence      NA       NA          8687
    ## 3532        472368  occurrence      NA       NA         46939
    ## 3705        597001  occurrence      NA       NA         63278
    ## 3845        598668  occurrence      NA       NA         63445
    ## 3846        598669  occurrence      NA       NA         63445
    ## 3856        598682  occurrence      NA       NA         63444
    ## 3868        601765  occurrence      NA       NA         63971
    ## 3883        601781  occurrence      NA       NA         63970
    ## 3891        601791  occurrence      NA       NA         63969
    ## 3916        601821  occurrence      NA       NA         63966
    ## 3939        601859  occurrence      NA       NA         63957
    ## 3953        601876  occurrence      NA       NA         63958
    ## 3976        601904  occurrence      NA       NA         63962
    ## 3986        601914  occurrence      NA       NA         63963
    ## 4002        601931  occurrence      NA       NA         63964
    ## 4043        703606  occurrence      NA       NA         75542
    ## 4114        716452  occurrence      NA       NA         76909
    ## 4135        718084  occurrence      NA       NA         77083
    ## 4139        718147  occurrence      NA       NA         77097
    ## 4259        916255  occurrence      NA       NA        104858
    ## 4260        916256  occurrence      NA       NA        104858
    ## 4272        916270  occurrence      NA       NA        104860
    ## 4274        916272  occurrence      NA       NA        104860
    ## 4324        955094  occurrence      NA       NA        111713
    ## 4364        969095  occurrence      NA       NA        114846
    ## 4374        969126  occurrence      NA       NA        114847
    ## 4375        969127  occurrence      NA       NA        114847
    ## 4390        969150  occurrence      NA       NA        114849
    ## 4398        969158  occurrence      NA       NA        114850
    ## 4409        969170  occurrence      NA       NA        114851
    ## 4420        969191  occurrence      NA       NA        114852
    ## 4421        969192  occurrence      NA       NA        114852
    ## 4426        969198  occurrence      NA       NA        114853
    ## 4430        969203  occurrence      NA       NA        114854
    ## 4438        969212  occurrence      NA       NA        114856
    ## 4448        969234  occurrence      NA       NA        114859
    ## 4454        969241  occurrence      NA       NA        114860
    ## 4455        969242  occurrence      NA       NA        114860
    ## 4563       1139580  occurrence      NA       NA        145216
    ## 4584       1139601  occurrence      NA       NA        145219
    ## 4585       1139602  occurrence      NA       NA        145220
    ## 4592       1139609  occurrence      NA       NA        145219
    ## 4593       1139610  occurrence      NA       NA        145220
    ## 4629       1139647  occurrence      NA       NA        145222
    ## 4663       1139687  occurrence      NA       NA        145227
    ## 4674       1139699  occurrence      NA       NA        145230
    ## 4675       1139700  occurrence      NA       NA        145230
    ## 4677       1139702  occurrence      NA       NA        145231
    ## 4687       1139723  occurrence      NA       NA        145233
    ## 4696       1139734  occurrence      NA       NA        145236
    ## 4727       1139765  occurrence      NA       NA        145240
    ## 4749       1140638  occurrence      NA       NA        145328
    ## 4752       1140641  occurrence      NA       NA        145329
    ## 4766       1140655  occurrence      NA       NA        145331
    ## 4783       1141839  occurrence      NA       NA        145466
    ## 4784       1141840  occurrence      NA       NA        145467
    ## 4785       1141841  occurrence      NA       NA        145468
    ## 4786       1141842  occurrence      NA       NA        145469
    ## 4930       1141991  occurrence      NA       NA        145492
    ## 4931       1141992  occurrence      NA       NA        145496
    ## 4932       1141993  occurrence      NA       NA        145498
    ## 4933       1141994  occurrence      NA       NA        145489
    ## 4934       1141995  occurrence      NA       NA        145490
    ## 4935       1141996  occurrence      NA       NA        145494
    ## 4965       1142801  occurrence      NA       NA        145513
    ## 4998       1143447  occurrence      NA       NA        145536
    ## 5136       1143794  occurrence      NA       NA        145590
    ## 5137       1143795  occurrence      NA       NA        145590
    ## 5138       1143796  occurrence      NA       NA        145590
    ## 5139       1143797  occurrence      NA       NA        145590
    ## 5156       1143814  occurrence      NA       NA        145591
    ## 5157       1143815  occurrence      NA       NA        145591
    ## 5158       1143816  occurrence      NA       NA        145591
    ## 5169       1143827  occurrence      NA       NA        145592
    ## 5179       1143839  occurrence      NA       NA        145595
    ## 5180       1143840  occurrence      NA       NA        145595
    ## 5181       1143841  occurrence      NA       NA        145595
    ## 5198       1143858  occurrence      NA       NA        145596
    ## 5339       1144111  occurrence      NA       NA        145651
    ## 5372       1144149  occurrence      NA       NA        145656
    ## 5813       1179391  occurrence      NA       NA        151959
    ## 5829       1185466  occurrence      NA       NA        152991
    ## 5833       1186608  occurrence      NA       NA        153323
    ##                                 identified_name identified_rank
    ## 33                            Glyptograptus sp.           genus
    ## 49                            Glyptograptus sp.           genus
    ## 51                            Glyptograptus sp.           genus
    ## 62                            Glyptograptus sp.           genus
    ## 80                            Glyptograptus sp.           genus
    ## 165                           Glyptograptus sp.           genus
    ## 197                           Glyptograptus sp.           genus
    ## 211                           Glyptograptus sp.           genus
    ## 225                        Monograptidae indet.          family
    ## 230                           Glyptograptus sp.           genus
    ## 238               Glyptograptus tamariscus aff.         species
    ## 241                    Glyptograptus nikolayevi         species
    ## 245               Glyptograptus tamariscus aff.         species
    ## 255                           Glyptograptus sp.           genus
    ## 278                           Glyptograptus sp.           genus
    ## 285                           Glyptograptus sp.           genus
    ## 289                           Glyptograptus sp.           genus
    ## 295                           Glyptograptus sp.           genus
    ## 307                           Glyptograptus sp.           genus
    ## 316                           Glyptograptus sp.           genus
    ## 325                           Glyptograptus sp.           genus
    ## 333                           Glyptograptus sp.           genus
    ## 360                           Glyptograptus sp.           genus
    ## 408                 Glyptograptus teretiusculus         species
    ## 413                           Glyptograptus sp.           genus
    ## 417                           Glyptograptus sp.           genus
    ## 424                           Glyptograptus sp.           genus
    ## 426                           Glyptograptus sp.           genus
    ## 427                           Glyptograptus sp.           genus
    ## 428                           Glyptograptus sp.           genus
    ## 440             Glyptograptus teretiusculus cf.         species
    ## 448                           Glyptograptus sp.           genus
    ## 476                           Glyptograptus sp.           genus
    ## 484                           Glyptograptus sp.           genus
    ## 492                           Glyptograptus sp.           genus
    ## 498                           Glyptograptus sp.           genus
    ## 513                           Glyptograptus sp.           genus
    ## 531                           Glyptograptus sp.           genus
    ## 536                           Glyptograptus sp.           genus
    ## 548                           Glyptograptus sp.           genus
    ## 550                           Glyptograptus sp.           genus
    ## 552                           Glyptograptus sp.           genus
    ## 556                           Glyptograptus sp.           genus
    ## 584                           Glyptograptus sp.           genus
    ## 592                           Glyptograptus sp.           genus
    ## 597                           Glyptograptus sp.           genus
    ## 636                           Glyptograptus sp.           genus
    ## 645                           Glyptograptus sp.           genus
    ## 647                           Glyptograptus sp.           genus
    ## 673                           Glyptograptus sp.           genus
    ## 676                           Glyptograptus sp.           genus
    ## 679                           Glyptograptus sp.           genus
    ## 695                           Glyptograptus sp.           genus
    ## 700                           Glyptograptus sp.           genus
    ## 707                           Glyptograptus sp.           genus
    ## 726                           Glyptograptus sp.           genus
    ## 749                           Glyptograptus sp.           genus
    ## 752                           Glyptograptus sp.           genus
    ## 779                           Glyptograptus sp.           genus
    ## 800                           Glyptograptus sp.           genus
    ## 815                           Glyptograptus sp.           genus
    ## 817                           Glyptograptus sp.           genus
    ## 829                           Glyptograptus sp.           genus
    ## 844                           Glyptograptus sp.           genus
    ## 845                           Glyptograptus sp.           genus
    ## 859                           Glyptograptus sp.           genus
    ## 867                           Glyptograptus sp.           genus
    ## 895                           Glyptograptus sp.           genus
    ## 905                           Glyptograptus sp.           genus
    ## 939                           Glyptograptus sp.           genus
    ## 951                           Glyptograptus sp.           genus
    ## 970                           Glyptograptus sp.           genus
    ## 979                           Glyptograptus sp.           genus
    ## 1005                          Glyptograptus sp.           genus
    ## 1015                          Glyptograptus sp.           genus
    ## 1022                          Glyptograptus sp.           genus
    ## 1038                          Glyptograptus sp.           genus
    ## 1045                          Glyptograptus sp.           genus
    ## 1061                          Glyptograptus sp.           genus
    ## 1073                          Glyptograptus sp.           genus
    ## 1096                          Glyptograptus sp.           genus
    ## 1111                          Glyptograptus sp.           genus
    ## 1144                          Glyptograptus sp.           genus
    ## 1153                          Glyptograptus sp.           genus
    ## 1178                          Glyptograptus sp.           genus
    ## 1184                          Glyptograptus sp.           genus
    ## 1188                          Glyptograptus sp.           genus
    ## 1195                          Glyptograptus sp.           genus
    ## 1202                          Glyptograptus sp.           genus
    ## 1207                          Glyptograptus sp.           genus
    ## 1239                          Glyptograptus sp.           genus
    ## 1256                          Glyptograptus sp.           genus
    ## 1262                          Glyptograptus sp.           genus
    ## 1275                          Glyptograptus sp.           genus
    ## 1294                          Glyptograptus sp.           genus
    ## 1297                          Glyptograptus sp.           genus
    ## 1329                          Glyptograptus sp.           genus
    ## 1341                          Glyptograptus sp.           genus
    ## 1365                          Glyptograptus sp.           genus
    ## 1388                          Glyptograptus sp.           genus
    ## 1409                          Glyptograptus sp.           genus
    ## 1418                        Glyptograptus " sp.           genus
    ## 1426                          Glyptograptus sp.           genus
    ## 1438                          Glyptograptus sp.           genus
    ## 1443                          Glyptograptus sp.           genus
    ## 1474                          Glyptograptus sp.           genus
    ## 1476                          Glyptograptus sp.           genus
    ## 1594                          Glyptograptus sp.           genus
    ## 1607                   Glyptograptus tamariscus         species
    ## 1614                     Glyptograptus sinuatus         species
    ## 1664               Glyptograptus auritus n. sp.         species
    ## 2131                          Glyptograptus sp.           genus
    ## 2145                          Glyptograptus sp.           genus
    ## 2154                          Glyptograptus sp.           genus
    ## 2163                          Glyptograptus sp.           genus
    ## 2167                          Glyptograptus sp.           genus
    ## 2178                          Glyptograptus sp.           genus
    ## 2187                          Glyptograptus sp.           genus
    ## 2193                          Glyptograptus sp.           genus
    ## 2197                          Glyptograptus sp.           genus
    ## 2217                          Glyptograptus sp.           genus
    ## 2236                          Glyptograptus sp.           genus
    ## 2242                          Glyptograptus sp.           genus
    ## 2249                          Glyptograptus sp.           genus
    ## 2259                          Glyptograptus sp.           genus
    ## 2287                          Glyptograptus sp.           genus
    ## 2340                          Glyptograptus sp.           genus
    ## 2343                          Glyptograptus sp.           genus
    ## 2355                          Glyptograptus sp.           genus
    ## 2360                          Glyptograptus sp.           genus
    ## 2367                          Glyptograptus sp.           genus
    ## 2370                          Glyptograptus sp.           genus
    ## 2382                          Glyptograptus sp.           genus
    ## 2415                          Glyptograptus sp.           genus
    ## 2417                          Glyptograptus sp.           genus
    ## 2427          Glyptograptus lorrainensis ex gr.         species
    ## 2428                          Glyptograptus sp.           genus
    ## 2429          Glyptograptus lorrainensis ex gr.         species
    ## 2445          Glyptograptus lorrainensis ex gr.         species
    ## 2452          Glyptograptus lorrainensis ex gr.         species
    ## 2454          Glyptograptus lorrainensis ex gr.         species
    ## 2489                   Glyptograptus tamariscus         species
    ## 2499                       Monograptidae indet.          family
    ## 2513             Glyptograptus lorrainensis cf.         species
    ## 2515                 Glyptograptus lorrainensis         species
    ## 2516          Glyptograptus lorrainensis ex gr.         species
    ## 2517                       Monograptidae indet.          family
    ## 2529                          Glyptograptus sp.           genus
    ## 2538                Glyptograptus euglyphus cf.         species
    ## 2615                          Glyptograptus sp.           genus
    ## 2648                          Glyptograptus sp.           genus
    ## 2655                          Glyptograptus sp.           genus
    ## 2662                          Glyptograptus sp.           genus
    ## 2687                          Glyptograptus sp.           genus
    ## 2690                          Glyptograptus sp.           genus
    ## 2831                       Monograptidae indet.          family
    ## 2882                       Monograptidae indet.          family
    ## 2936              Glyptograptus tamariscus aff.         species
    ## 2937                       Monograptidae indet.          family
    ## 3028                       Monograptidae indet.          family
    ## 3102                          Glyptograptus sp.           genus
    ## 3106               Glyptograptus tamariscus cf.         species
    ## 3115              Glyptograptus tamariscus aff.         species
    ## 3125               Glyptograptus tamariscus cf.         species
    ## 3201                         Glyptograptus spp.           genus
    ## 3215                      Glyptograptus ultimus         species
    ## 3234                     Glyptograptus insertus         species
    ## 3235                   Glyptograptus tamariscus         species
    ## 3275                          Glyptograptus sp.           genus
    ## 3301                          Glyptograptus sp.           genus
    ## 3305               Glyptograptus tamariscus cf.         species
    ## 3306                          Glyptograptus sp.           genus
    ## 3363                   Glyptograptus tamariscus         species
    ## 3364                          Glyptograptus sp.           genus
    ## 3378                          Glyptograptus sp.           genus
    ## 3456    Glyptograptus (Pseudoglyptograptus) vas         species
    ## 3457    Glyptograptus (Pseudoglyptograptus) vas         species
    ## 3470                          Glyptograptus sp.           genus
    ## 3477                          Glyptograptus sp.           genus
    ## 3487                          Glyptograptus sp.           genus
    ## 3506                          Glyptograptus sp.           genus
    ## 3532                Glyptograptus teretiusculus         species
    ## 3705               Glyptograptus austrodentatus         species
    ## 3845            Glyptograptus teretiusculus cf.         species
    ## 3846                          Glyptograptus sp.           genus
    ## 3856            Glyptograptus teretiusculus cf.         species
    ## 3868                Glyptograptus teretiusculus         species
    ## 3883            Glyptograptus teretiusculus cf.         species
    ## 3891                          Glyptograptus sp.           genus
    ## 3916                Glyptograptus teretiusculus         species
    ## 3939                Glyptograptus teretiusculus         species
    ## 3953                Glyptograptus teretiusculus         species
    ## 3976                     Glyptograptus schaferi         species
    ## 3986            Glyptograptus teretiusculus cf.         species
    ## 4002            Glyptograptus teretiusculus cf.         species
    ## 4043                          Glyptograptus sp.           genus
    ## 4114            Glyptograptus teretiusculus cf.         species
    ## 4135            Glyptograptus teretiusculus cf.         species
    ## 4139            Glyptograptus teretiusculus cf.         species
    ## 4259                     Glyptograptus dentatus         species
    ## 4260                          Glyptograptus sp.           genus
    ## 4272                 Glyptograptus dentatus cf.         species
    ## 4274                          Glyptograptus sp.           genus
    ## 4324 Diplograptus (Glyptograptus) teretiusculus         species
    ## 4364                          Glyptograptus sp.           genus
    ## 4374                Glyptograptus teretiusculus         species
    ## 4375                          Glyptograptus sp.           genus
    ## 4390                          Glyptograptus sp.           genus
    ## 4398                Glyptograptus teretiusculus         species
    ## 4409                          Glyptograptus sp.           genus
    ## 4420              Glyptograptus teretiusculus ?         species
    ## 4421                          Glyptograptus sp.           genus
    ## 4426                          Glyptograptus sp.           genus
    ## 4430                          Glyptograptus sp.           genus
    ## 4438                          Glyptograptus sp.           genus
    ## 4448                          Glyptograptus sp.           genus
    ## 4454                 Glyptograptus teretisculus         species
    ## 4455                          Glyptograptus sp.           genus
    ## 4563                       Glyptograptus avitus         species
    ## 4584                Glyptograptus incertus aff.         species
    ## 4585                Glyptograptus incertus aff.         species
    ## 4592                   Glyptograptus tamariscus         species
    ## 4593                   Glyptograptus tamariscus         species
    ## 4629                   Glyptograptus enodis cf.         species
    ## 4663                          Glyptograptus sp.           genus
    ## 4674                Glyptograptus euglyphus cf.         species
    ## 4675                Glyptograptus teretiusculus         species
    ## 4677                Glyptograptus teretiusculus         species
    ## 4687                Glyptograptus euglyphus cf.         species
    ## 4696                Glyptograptus euglyphus cf.         species
    ## 4727                      Glyptograptus sp. cf.           genus
    ## 4749                          Glyptograptus sp.           genus
    ## 4752                          Glyptograptus sp.           genus
    ## 4766                    Glyptograptus euglyphus         species
    ## 4783                Glyptograptus euglyphus cf.         species
    ## 4784                Glyptograptus euglyphus cf.         species
    ## 4785                Glyptograptus euglyphus cf.         species
    ## 4786                          Glyptograptus sp.           genus
    ## 4930                        Glyptograptus altus         species
    ## 4931                   Glyptograptus tamariscus         species
    ## 4932                   Glyptograptus tamariscus         species
    ## 4933            Glyptograptus teretiusculus cf.         species
    ## 4934                          Glyptograptus sp.           genus
    ## 4935                          Glyptograptus sp.           genus
    ## 4965               Glyptograptus tamariscus cf.         species
    ## 4998              Glyptograptus tamariscus aff.         species
    ## 5136                   Glyptograptus enodis cf.         species
    ## 5137                       Glyptograptus gnomus         species
    ## 5138                     Glyptograptus incertus         species
    ## 5139                   Glyptograptus tamariscus         species
    ## 5156                   Glyptograptus laciniosus         species
    ## 5157                    Glyptograptus lanpherei         species
    ## 5158                   Glyptograptus tamariscus         species
    ## 5169               Glyptograptus tamariscus cf.         species
    ## 5179                   Glyptograptus enodis cf.         species
    ## 5180                   Glyptograptus laciniosus         species
    ## 5181               Glyptograptus tamariscus cf.         species
    ## 5198                   Glyptograptus laciniosus         species
    ## 5339                          Glyptograptus sp.           genus
    ## 5372                 Glyptograptus incertus cf.         species
    ## 5813                 Glyptograptus serratus cf.         species
    ## 5829                   Glyptograptus tamariscus         species
    ## 5833                  Glyptograptus lungmaensis         species
    ##      identified_no        taxonomic_reason accepted_name accepted_rank
    ## 33           33669                    <NA> Glyptograptus         genus
    ## 49           33669                    <NA> Glyptograptus         genus
    ## 51           33669                    <NA> Glyptograptus         genus
    ## 62           33669                    <NA> Glyptograptus         genus
    ## 80           33669                    <NA> Glyptograptus         genus
    ## 165          33669                    <NA> Glyptograptus         genus
    ## 197          33669                    <NA> Glyptograptus         genus
    ## 211          33669                    <NA> Glyptograptus         genus
    ## 225         306248                    <NA> Monograptidae        family
    ## 230          33669                    <NA> Glyptograptus         genus
    ## 238          33669 taxon not fully entered Glyptograptus         genus
    ## 241          33669 taxon not fully entered Glyptograptus         genus
    ## 245          33669 taxon not fully entered Glyptograptus         genus
    ## 255          33669                    <NA> Glyptograptus         genus
    ## 278          33669                    <NA> Glyptograptus         genus
    ## 285          33669                    <NA> Glyptograptus         genus
    ## 289          33669                    <NA> Glyptograptus         genus
    ## 295          33669                    <NA> Glyptograptus         genus
    ## 307          33669                    <NA> Glyptograptus         genus
    ## 316          33669                    <NA> Glyptograptus         genus
    ## 325          33669                    <NA> Glyptograptus         genus
    ## 333          33669                    <NA> Glyptograptus         genus
    ## 360          33669                    <NA> Glyptograptus         genus
    ## 408          33669 taxon not fully entered Glyptograptus         genus
    ## 413          33669                    <NA> Glyptograptus         genus
    ## 417          33669                    <NA> Glyptograptus         genus
    ## 424          33669                    <NA> Glyptograptus         genus
    ## 426          33669                    <NA> Glyptograptus         genus
    ## 427          33669                    <NA> Glyptograptus         genus
    ## 428          33669                    <NA> Glyptograptus         genus
    ## 440          33669 taxon not fully entered Glyptograptus         genus
    ## 448          33669                    <NA> Glyptograptus         genus
    ## 476          33669                    <NA> Glyptograptus         genus
    ## 484          33669                    <NA> Glyptograptus         genus
    ## 492          33669                    <NA> Glyptograptus         genus
    ## 498          33669                    <NA> Glyptograptus         genus
    ## 513          33669                    <NA> Glyptograptus         genus
    ## 531          33669                    <NA> Glyptograptus         genus
    ## 536          33669                    <NA> Glyptograptus         genus
    ## 548          33669                    <NA> Glyptograptus         genus
    ## 550          33669                    <NA> Glyptograptus         genus
    ## 552          33669                    <NA> Glyptograptus         genus
    ## 556          33669                    <NA> Glyptograptus         genus
    ## 584          33669                    <NA> Glyptograptus         genus
    ## 592          33669                    <NA> Glyptograptus         genus
    ## 597          33669                    <NA> Glyptograptus         genus
    ## 636          33669                    <NA> Glyptograptus         genus
    ## 645          33669                    <NA> Glyptograptus         genus
    ## 647          33669                    <NA> Glyptograptus         genus
    ## 673          33669                    <NA> Glyptograptus         genus
    ## 676          33669                    <NA> Glyptograptus         genus
    ## 679          33669                    <NA> Glyptograptus         genus
    ## 695          33669                    <NA> Glyptograptus         genus
    ## 700          33669                    <NA> Glyptograptus         genus
    ## 707          33669                    <NA> Glyptograptus         genus
    ## 726          33669                    <NA> Glyptograptus         genus
    ## 749          33669                    <NA> Glyptograptus         genus
    ## 752          33669                    <NA> Glyptograptus         genus
    ## 779          33669                    <NA> Glyptograptus         genus
    ## 800          33669                    <NA> Glyptograptus         genus
    ## 815          33669                    <NA> Glyptograptus         genus
    ## 817          33669                    <NA> Glyptograptus         genus
    ## 829          33669                    <NA> Glyptograptus         genus
    ## 844          33669                    <NA> Glyptograptus         genus
    ## 845          33669                    <NA> Glyptograptus         genus
    ## 859          33669                    <NA> Glyptograptus         genus
    ## 867          33669                    <NA> Glyptograptus         genus
    ## 895          33669                    <NA> Glyptograptus         genus
    ## 905          33669                    <NA> Glyptograptus         genus
    ## 939          33669                    <NA> Glyptograptus         genus
    ## 951          33669                    <NA> Glyptograptus         genus
    ## 970          33669                    <NA> Glyptograptus         genus
    ## 979          33669                    <NA> Glyptograptus         genus
    ## 1005         33669                    <NA> Glyptograptus         genus
    ## 1015         33669                    <NA> Glyptograptus         genus
    ## 1022         33669                    <NA> Glyptograptus         genus
    ## 1038         33669                    <NA> Glyptograptus         genus
    ## 1045         33669                    <NA> Glyptograptus         genus
    ## 1061         33669                    <NA> Glyptograptus         genus
    ## 1073         33669                    <NA> Glyptograptus         genus
    ## 1096         33669                    <NA> Glyptograptus         genus
    ## 1111         33669                    <NA> Glyptograptus         genus
    ## 1144         33669                    <NA> Glyptograptus         genus
    ## 1153         33669                    <NA> Glyptograptus         genus
    ## 1178         33669                    <NA> Glyptograptus         genus
    ## 1184         33669                    <NA> Glyptograptus         genus
    ## 1188         33669                    <NA> Glyptograptus         genus
    ## 1195         33669                    <NA> Glyptograptus         genus
    ## 1202         33669                    <NA> Glyptograptus         genus
    ## 1207         33669                    <NA> Glyptograptus         genus
    ## 1239         33669                    <NA> Glyptograptus         genus
    ## 1256         33669                    <NA> Glyptograptus         genus
    ## 1262         33669                    <NA> Glyptograptus         genus
    ## 1275         33669                    <NA> Glyptograptus         genus
    ## 1294         33669                    <NA> Glyptograptus         genus
    ## 1297         33669                    <NA> Glyptograptus         genus
    ## 1329         33669                    <NA> Glyptograptus         genus
    ## 1341         33669                    <NA> Glyptograptus         genus
    ## 1365         33669                    <NA> Glyptograptus         genus
    ## 1388         33669                    <NA> Glyptograptus         genus
    ## 1409         33669                    <NA> Glyptograptus         genus
    ## 1418         33669                    <NA> Glyptograptus         genus
    ## 1426         33669                    <NA> Glyptograptus         genus
    ## 1438         33669                    <NA> Glyptograptus         genus
    ## 1443         33669                    <NA> Glyptograptus         genus
    ## 1474         33669                    <NA> Glyptograptus         genus
    ## 1476         33669                    <NA> Glyptograptus         genus
    ## 1594         33669                    <NA> Glyptograptus         genus
    ## 1607         33669 taxon not fully entered Glyptograptus         genus
    ## 1614         33669 taxon not fully entered Glyptograptus         genus
    ## 1664         33669 taxon not fully entered Glyptograptus         genus
    ## 2131         33669                    <NA> Glyptograptus         genus
    ## 2145         33669                    <NA> Glyptograptus         genus
    ## 2154         33669                    <NA> Glyptograptus         genus
    ## 2163         33669                    <NA> Glyptograptus         genus
    ## 2167         33669                    <NA> Glyptograptus         genus
    ## 2178         33669                    <NA> Glyptograptus         genus
    ## 2187         33669                    <NA> Glyptograptus         genus
    ## 2193         33669                    <NA> Glyptograptus         genus
    ## 2197         33669                    <NA> Glyptograptus         genus
    ## 2217         33669                    <NA> Glyptograptus         genus
    ## 2236         33669                    <NA> Glyptograptus         genus
    ## 2242         33669                    <NA> Glyptograptus         genus
    ## 2249         33669                    <NA> Glyptograptus         genus
    ## 2259         33669                    <NA> Glyptograptus         genus
    ## 2287         33669                    <NA> Glyptograptus         genus
    ## 2340         33669                    <NA> Glyptograptus         genus
    ## 2343         33669                    <NA> Glyptograptus         genus
    ## 2355         33669                    <NA> Glyptograptus         genus
    ## 2360         33669                    <NA> Glyptograptus         genus
    ## 2367         33669                    <NA> Glyptograptus         genus
    ## 2370         33669                    <NA> Glyptograptus         genus
    ## 2382         33669                    <NA> Glyptograptus         genus
    ## 2415         33669                    <NA> Glyptograptus         genus
    ## 2417         33669                    <NA> Glyptograptus         genus
    ## 2427         33669 taxon not fully entered Glyptograptus         genus
    ## 2428         33669                    <NA> Glyptograptus         genus
    ## 2429         33669 taxon not fully entered Glyptograptus         genus
    ## 2445         33669 taxon not fully entered Glyptograptus         genus
    ## 2452         33669 taxon not fully entered Glyptograptus         genus
    ## 2454         33669 taxon not fully entered Glyptograptus         genus
    ## 2489         33669 taxon not fully entered Glyptograptus         genus
    ## 2499        306248                    <NA> Monograptidae        family
    ## 2513         33669 taxon not fully entered Glyptograptus         genus
    ## 2515         33669 taxon not fully entered Glyptograptus         genus
    ## 2516         33669 taxon not fully entered Glyptograptus         genus
    ## 2517        306248                    <NA> Monograptidae        family
    ## 2529         33669                    <NA> Glyptograptus         genus
    ## 2538         33669 taxon not fully entered Glyptograptus         genus
    ## 2615         33669                    <NA> Glyptograptus         genus
    ## 2648         33669                    <NA> Glyptograptus         genus
    ## 2655         33669                    <NA> Glyptograptus         genus
    ## 2662         33669                    <NA> Glyptograptus         genus
    ## 2687         33669                    <NA> Glyptograptus         genus
    ## 2690         33669                    <NA> Glyptograptus         genus
    ## 2831        306248                    <NA> Monograptidae        family
    ## 2882        306248                    <NA> Monograptidae        family
    ## 2936         33669 taxon not fully entered Glyptograptus         genus
    ## 2937        306248                    <NA> Monograptidae        family
    ## 3028        306248                    <NA> Monograptidae        family
    ## 3102         33669                    <NA> Glyptograptus         genus
    ## 3106         33669 taxon not fully entered Glyptograptus         genus
    ## 3115         33669 taxon not fully entered Glyptograptus         genus
    ## 3125         33669 taxon not fully entered Glyptograptus         genus
    ## 3201         33669                    <NA> Glyptograptus         genus
    ## 3215         33669 taxon not fully entered Glyptograptus         genus
    ## 3234         33669 taxon not fully entered Glyptograptus         genus
    ## 3235         33669 taxon not fully entered Glyptograptus         genus
    ## 3275         33669                    <NA> Glyptograptus         genus
    ## 3301         33669                    <NA> Glyptograptus         genus
    ## 3305         33669 taxon not fully entered Glyptograptus         genus
    ## 3306         33669                    <NA> Glyptograptus         genus
    ## 3363         33669 taxon not fully entered Glyptograptus         genus
    ## 3364         33669                    <NA> Glyptograptus         genus
    ## 3378         33669                    <NA> Glyptograptus         genus
    ## 3456         33669 taxon not fully entered Glyptograptus         genus
    ## 3457         33669 taxon not fully entered Glyptograptus         genus
    ## 3470         33669                    <NA> Glyptograptus         genus
    ## 3477         33669                    <NA> Glyptograptus         genus
    ## 3487         33669                    <NA> Glyptograptus         genus
    ## 3506         33669                    <NA> Glyptograptus         genus
    ## 3532         33669 taxon not fully entered Glyptograptus         genus
    ## 3705         33669 taxon not fully entered Glyptograptus         genus
    ## 3845         33669 taxon not fully entered Glyptograptus         genus
    ## 3846         33669                    <NA> Glyptograptus         genus
    ## 3856         33669 taxon not fully entered Glyptograptus         genus
    ## 3868         33669 taxon not fully entered Glyptograptus         genus
    ## 3883         33669 taxon not fully entered Glyptograptus         genus
    ## 3891         33669                    <NA> Glyptograptus         genus
    ## 3916         33669 taxon not fully entered Glyptograptus         genus
    ## 3939         33669 taxon not fully entered Glyptograptus         genus
    ## 3953         33669 taxon not fully entered Glyptograptus         genus
    ## 3976         33669 taxon not fully entered Glyptograptus         genus
    ## 3986         33669 taxon not fully entered Glyptograptus         genus
    ## 4002         33669 taxon not fully entered Glyptograptus         genus
    ## 4043         33669                    <NA> Glyptograptus         genus
    ## 4114         33669 taxon not fully entered Glyptograptus         genus
    ## 4135         33669 taxon not fully entered Glyptograptus         genus
    ## 4139         33669 taxon not fully entered Glyptograptus         genus
    ## 4259         33669 taxon not fully entered Glyptograptus         genus
    ## 4260         33669                    <NA> Glyptograptus         genus
    ## 4272         33669 taxon not fully entered Glyptograptus         genus
    ## 4274         33669                    <NA> Glyptograptus         genus
    ## 4324        306246             rank change Glyptograptus         genus
    ## 4364         33669                    <NA> Glyptograptus         genus
    ## 4374         33669 taxon not fully entered Glyptograptus         genus
    ## 4375         33669                    <NA> Glyptograptus         genus
    ## 4390         33669                    <NA> Glyptograptus         genus
    ## 4398         33669 taxon not fully entered Glyptograptus         genus
    ## 4409         33669                    <NA> Glyptograptus         genus
    ## 4420         33669 taxon not fully entered Glyptograptus         genus
    ## 4421         33669                    <NA> Glyptograptus         genus
    ## 4426         33669                    <NA> Glyptograptus         genus
    ## 4430         33669                    <NA> Glyptograptus         genus
    ## 4438         33669                    <NA> Glyptograptus         genus
    ## 4448         33669                    <NA> Glyptograptus         genus
    ## 4454         33669 taxon not fully entered Glyptograptus         genus
    ## 4455         33669                    <NA> Glyptograptus         genus
    ## 4563         33669 taxon not fully entered Glyptograptus         genus
    ## 4584         33669 taxon not fully entered Glyptograptus         genus
    ## 4585         33669 taxon not fully entered Glyptograptus         genus
    ## 4592         33669 taxon not fully entered Glyptograptus         genus
    ## 4593         33669 taxon not fully entered Glyptograptus         genus
    ## 4629         33669 taxon not fully entered Glyptograptus         genus
    ## 4663         33669                    <NA> Glyptograptus         genus
    ## 4674         33669 taxon not fully entered Glyptograptus         genus
    ## 4675         33669 taxon not fully entered Glyptograptus         genus
    ## 4677         33669 taxon not fully entered Glyptograptus         genus
    ## 4687         33669 taxon not fully entered Glyptograptus         genus
    ## 4696         33669 taxon not fully entered Glyptograptus         genus
    ## 4727         33669                    <NA> Glyptograptus         genus
    ## 4749         33669                    <NA> Glyptograptus         genus
    ## 4752         33669                    <NA> Glyptograptus         genus
    ## 4766         33669 taxon not fully entered Glyptograptus         genus
    ## 4783         33669 taxon not fully entered Glyptograptus         genus
    ## 4784         33669 taxon not fully entered Glyptograptus         genus
    ## 4785         33669 taxon not fully entered Glyptograptus         genus
    ## 4786         33669                    <NA> Glyptograptus         genus
    ## 4930         33669 taxon not fully entered Glyptograptus         genus
    ## 4931         33669 taxon not fully entered Glyptograptus         genus
    ## 4932         33669 taxon not fully entered Glyptograptus         genus
    ## 4933         33669 taxon not fully entered Glyptograptus         genus
    ## 4934         33669                    <NA> Glyptograptus         genus
    ## 4935         33669                    <NA> Glyptograptus         genus
    ## 4965         33669 taxon not fully entered Glyptograptus         genus
    ## 4998         33669 taxon not fully entered Glyptograptus         genus
    ## 5136         33669 taxon not fully entered Glyptograptus         genus
    ## 5137         33669 taxon not fully entered Glyptograptus         genus
    ## 5138         33669 taxon not fully entered Glyptograptus         genus
    ## 5139         33669 taxon not fully entered Glyptograptus         genus
    ## 5156         33669 taxon not fully entered Glyptograptus         genus
    ## 5157         33669 taxon not fully entered Glyptograptus         genus
    ## 5158         33669 taxon not fully entered Glyptograptus         genus
    ## 5169         33669 taxon not fully entered Glyptograptus         genus
    ## 5179         33669 taxon not fully entered Glyptograptus         genus
    ## 5180         33669 taxon not fully entered Glyptograptus         genus
    ## 5181         33669 taxon not fully entered Glyptograptus         genus
    ## 5198         33669 taxon not fully entered Glyptograptus         genus
    ## 5339         33669                    <NA> Glyptograptus         genus
    ## 5372         33669 taxon not fully entered Glyptograptus         genus
    ## 5813         33669 taxon not fully entered Glyptograptus         genus
    ## 5829         33669 taxon not fully entered Glyptograptus         genus
    ## 5833         33669 taxon not fully entered Glyptograptus         genus
    ##      accepted_no    early_interval     late_interval early_age late_age
    ## 33         33669      Whiterockian      Whiterockian     471.8    457.5
    ## 49         33669          Llanvirn          Llanvirn     466.0    460.9
    ## 51         33669         Llandeilo         Llandeilo     466.0    449.5
    ## 62         33669       Black River       Black River     460.9    457.5
    ## 80         33669        Ordovician        Ordovician     485.4    443.4
    ## 165        33669        Llandovery        Llandovery     443.4    433.4
    ## 197        33669        Shermanian        Shermanian     460.9    449.5
    ## 211        33669         Eastonian         Eastonian     456.1    449.5
    ## 225       306248        Llandovery        Llandovery     443.4    433.4
    ## 230        33669         Eastonian            Onnian     456.1    449.5
    ## 238        33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 241        33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 245        33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 255        33669     Marshbrookian          Actonian     455.8    452.0
    ## 278        33669     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 285        33669     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 289        33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 295        33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 307        33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 316        33669     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 325        33669            Arenig            Arenig     478.6    466.0
    ## 333        33669            Arenig            Arenig     478.6    466.0
    ## 360        33669         Costonian         Harnagian     460.9    455.8
    ## 408        33669         Dobrotiva         Dobrotiva     466.0    460.9
    ## 413        33669   Late Ordovician            Vinice     458.4    455.8
    ## 417        33669   Late Ordovician          Zahorany     458.4    455.8
    ## 424        33669         Rawtheyan      Kralodvorian     455.8    445.6
    ## 426        33669         Rawtheyan      Kralodvorian     455.8    445.6
    ## 427        33669         Rawtheyan      Kralodvorian     455.8    445.6
    ## 428        33669          Kosovian          Kosovian     445.6    443.7
    ## 440        33669 Middle Ordovician Middle Ordovician     470.0    458.4
    ## 448        33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 476        33669            Arenig            Arenig     478.6    466.0
    ## 484        33669    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 492        33669           Caradoc           Caradoc     460.9    449.5
    ## 498        33669           Caradoc           Caradoc     460.9    449.5
    ## 513        33669            Arenig            Arenig     478.6    466.0
    ## 531        33669          Llanvirn          Llanvirn     466.0    460.9
    ## 536        33669            Arenig            Arenig     478.6    466.0
    ## 548        33669         Llandeilo         Llandeilo     466.0    449.5
    ## 550        33669          Llanvirn          Llanvirn     466.0    460.9
    ## 552        33669           Ashgill           Ashgill     449.5    443.7
    ## 556        33669         Costonian     Marshbrookian     460.9    452.0
    ## 584        33669            Arenig            Arenig     478.6    466.0
    ## 592        33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 597        33669            Arenig            Arenig     478.6    466.0
    ## 636        33669         Rawtheyan            Wufeng     455.8    443.7
    ## 645        33669            Arenig            Arenig     478.6    466.0
    ## 647        33669            Arenig            Arenig     478.6    466.0
    ## 673        33669         Rawtheyan            Wufeng     455.8    443.7
    ## 676        33669         Llandeilo         Llandeilo     466.0    449.5
    ## 679        33669            Arenig            Arenig     478.6    466.0
    ## 695        33669            Arenig            Arenig     478.6    466.0
    ## 700        33669         Rawtheyan            Wufeng     455.8    443.7
    ## 707        33669            Arenig            Arenig     478.6    466.0
    ## 726        33669    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 749        33669            Arenig            Arenig     478.6    466.0
    ## 752        33669            Arenig            Arenig     478.6    466.0
    ## 779        33669          Llanvirn          Llanvirn     466.0    460.9
    ## 800        33669          Llanvirn          Llanvirn     466.0    460.9
    ## 815        33669            Arenig            Arenig     478.6    466.0
    ## 817        33669            Arenig            Arenig     478.6    466.0
    ## 829        33669         Llandeilo         Llandeilo     466.0    449.5
    ## 844        33669             Dawan             Dawan     478.6    468.1
    ## 845        33669            Arenig            Arenig     478.6    466.0
    ## 859        33669            Arenig            Arenig     478.6    466.0
    ## 867        33669    Late Llandeilo    Late Llandeilo     460.9    449.5
    ## 895        33669          Llanvirn          Llanvirn     466.0    460.9
    ## 905        33669            Arenig            Arenig     478.6    466.0
    ## 939        33669         Llandeilo         Llandeilo     466.0    449.5
    ## 951        33669            Wufeng        Hirnantian     449.5    443.4
    ## 970        33669         Llandeilo         Llandeilo     466.0    449.5
    ## 979        33669             Dawan             Dawan     478.6    468.1
    ## 1005       33669         Rawtheyan            Wufeng     455.8    443.7
    ## 1015       33669         Costonian         Harnagian     460.9    455.8
    ## 1022       33669              Hulo              Hulo     468.1    460.9
    ## 1038       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1045       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1061       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 1073       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1096       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 1111       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1144       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 1153       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1178       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 1184       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1188       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1195       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1202       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 1207       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1239       33669           Ningkuo           Ningkuo     478.6    468.1
    ## 1256       33669         Rawtheyan            Wufeng     455.8    443.7
    ## 1262       33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 1275       33669         Rawtheyan            Wufeng     455.8    443.7
    ## 1294       33669       Longvillian       Longvillian     457.5    455.8
    ## 1297       33669            Arenig            Arenig     478.6    466.0
    ## 1329       33669           Caradoc           Caradoc     460.9    449.5
    ## 1341       33669     Late Llanvirn     Late Llanvirn     463.5    460.9
    ## 1365       33669         Costonian       Longvillian     460.9    455.8
    ## 1388       33669    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 1409       33669         Costonian         Harnagian     460.9    455.8
    ## 1418       33669          Actonian            Onnian     455.8    449.5
    ## 1426       33669          Llanvirn          Llanvirn     466.0    460.9
    ## 1438       33669        Hirnantian        Hirnantian     445.2    443.4
    ## 1443       33669    Late Llandeilo    Late Llandeilo     460.9    449.5
    ## 1474       33669           Caradoc           Caradoc     460.9    449.5
    ## 1476       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 1594       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1607       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 1614       33669        Rhuddanian          Aeronian     443.4    438.5
    ## 1664       33669         Telychian         Telychian     438.5    433.4
    ## 2131       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 2145       33669         Harnagian     Marshbrookian     457.5    452.0
    ## 2154       33669         Costonian         Harnagian     460.9    455.8
    ## 2163       33669        Pusgillian        Pusgillian     449.5    445.6
    ## 2167       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 2178       33669         Costonian         Harnagian     460.9    455.8
    ## 2187       33669         Cautleyan        Hirnantian     449.5    443.4
    ## 2193       33669        Pusgillian        Pusgillian     449.5    445.6
    ## 2197       33669         Soudleyan     Marshbrookian     457.5    452.0
    ## 2217       33669           Caradoc           Caradoc     460.9    449.5
    ## 2236       33669         Cautleyan        Hirnantian     449.5    443.4
    ## 2242       33669         Soudleyan            Onnian     457.5    449.5
    ## 2249       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 2259       33669            Arenig            Arenig     478.6    466.0
    ## 2287       33669          Llanvirn         Llandeilo     466.0    449.5
    ## 2340       33669    Late Llandeilo    Late Llandeilo     460.9    449.5
    ## 2343       33669   Early Llandeilo   Early Llandeilo     466.0    460.9
    ## 2355       33669          Llanvirn          Llanvirn     466.0    460.9
    ## 2360       33669         Llandeilo           Caradoc     466.0    449.5
    ## 2367       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 2370       33669           Caradoc           Caradoc     460.9    449.5
    ## 2382       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 2415       33669           Ashgill        Llandovery     449.5    433.4
    ## 2417       33669        Caradocian        Caradocian     460.9    449.5
    ## 2427       33669           Ashgill           Ashgill     449.5    443.7
    ## 2428       33669           Ashgill           Ashgill     449.5    443.7
    ## 2429       33669           Ashgill           Ashgill     449.5    443.7
    ## 2445       33669           Ashgill           Ashgill     449.5    443.7
    ## 2452       33669           Ashgill           Ashgill     449.5    443.7
    ## 2454       33669           Ashgill           Ashgill     449.5    443.7
    ## 2489       33669        Llandovery        Llandovery     443.4    433.4
    ## 2499      306248        Llandovery        Llandovery     443.4    433.4
    ## 2513       33669 Middle Ordovician   Late Ordovician     470.0    443.4
    ## 2515       33669   Late Ordovician   Late Ordovician     458.4    443.4
    ## 2516       33669   Late Ordovician   Late Ordovician     458.4    443.4
    ## 2517      306248            Ludlow            Ludlow     427.4    423.0
    ## 2529       33669       Richmondian         Gamachian     449.5    443.7
    ## 2538       33669        Caradocian        Caradocian     460.9    449.5
    ## 2615       33669           Caradoc           Caradoc     460.9    449.5
    ## 2648       33669       Dobrotivian       Dobrotivian     460.9    457.5
    ## 2655       33669         Oretanian         Oretanian     466.0    460.9
    ## 2662       33669       Dobrotivian       Dobrotivian     460.9    457.5
    ## 2687       33669       Dobrotivian       Dobrotivian     460.9    457.5
    ## 2690       33669       Dobrotivian       Dobrotivian     460.9    457.5
    ## 2831      306248           Wenlock            Ludlow     433.4    423.0
    ## 2882      306248           Pridoli        Helderberg     423.0    391.9
    ## 2936       33669          Aeronian          Aeronian     440.8    438.5
    ## 2937      306248          Aeronian          Aeronian     440.8    438.5
    ## 3028      306248           Pridoli        Helderberg     423.0    391.9
    ## 3102       33669        Llandovery        Llandovery     443.4    433.4
    ## 3106       33669        Llandovery        Llandovery     443.4    433.4
    ## 3115       33669        Llandovery        Llandovery     443.4    433.4
    ## 3125       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 3201       33669         Telychian         Telychian     438.5    433.4
    ## 3215       33669         Telychian         Telychian     438.5    433.4
    ## 3234       33669          Aeronian          Aeronian     440.8    438.5
    ## 3235       33669          Aeronian          Aeronian     440.8    438.5
    ## 3275       33669          Aeronian          Aeronian     440.8    438.5
    ## 3301       33669        Llandovery        Llandovery     443.4    433.4
    ## 3305       33669        Llandovery        Llandovery     443.4    433.4
    ## 3306       33669        Llandovery        Llandovery     443.4    433.4
    ## 3363       33669        Llandovery        Llandovery     443.4    433.4
    ## 3364       33669        Llandovery        Llandovery     443.4    433.4
    ## 3378       33669           Ashgill           Ashgill     449.5    443.7
    ## 3456       33669        Llandovery        Llandovery     443.4    433.4
    ## 3457       33669        Llandovery        Llandovery     443.4    433.4
    ## 3470       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 3477       33669          Llanvirn          Llanvirn     466.0    460.9
    ## 3487       33669    Early Llanvirn    Early Llanvirn     466.0    463.5
    ## 3506       33669            Arenig            Arenig     478.6    466.0
    ## 3532       33669 Middle Ordovician   Late Ordovician     470.0    443.4
    ## 3705       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3845       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 3846       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 3856       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 3868       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3883       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3891       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 3916       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3939       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3953       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3976       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 3986       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 4002       33669       Darriwilian       Darriwilian     467.3    458.4
    ## 4043       33669            Wufeng            Wufeng     449.5    443.7
    ## 4114       33669           Caradoc           Caradoc     460.9    449.5
    ## 4135       33669           Caradoc           Caradoc     460.9    449.5
    ## 4139       33669         Llandeilo         Llandeilo     466.0    449.5
    ## 4259       33669      Whiterockian      Whiterockian     471.8    457.5
    ## 4260       33669      Whiterockian      Whiterockian     471.8    457.5
    ## 4272       33669      Whiterockian      Whiterockian     471.8    457.5
    ## 4274       33669      Whiterockian      Whiterockian     471.8    457.5
    ## 4324       33669   Late Ordovician   Late Ordovician     458.4    443.4
    ## 4364       33669        Caradocian        Caradocian     460.9    449.5
    ## 4374       33669        Caradocian        Caradocian     460.9    449.5
    ## 4375       33669        Caradocian        Caradocian     460.9    449.5
    ## 4390       33669        Caradocian        Caradocian     460.9    449.5
    ## 4398       33669        Caradocian        Caradocian     460.9    449.5
    ## 4409       33669        Caradocian        Caradocian     460.9    449.5
    ## 4420       33669        Caradocian        Caradocian     460.9    449.5
    ## 4421       33669        Caradocian        Caradocian     460.9    449.5
    ## 4426       33669        Caradocian        Caradocian     460.9    449.5
    ## 4430       33669        Caradocian        Caradocian     460.9    449.5
    ## 4438       33669        Caradocian        Caradocian     460.9    449.5
    ## 4448       33669       Llanvirnian       Llanvirnian     468.1    460.9
    ## 4454       33669       Llandeilian        Caradocian     466.0    449.5
    ## 4455       33669       Llandeilian        Caradocian     466.0    449.5
    ## 4563       33669        Hirnantian        Hirnantian     445.2    443.4
    ## 4584       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 4585       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 4592       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 4593       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 4629       33669          Aeronian          Aeronian     440.8    438.5
    ## 4663       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4674       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4675       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4677       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4687       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4696       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4727       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4749       33669       Llandeilian       Llandeilian     466.0    460.9
    ## 4752       33669       Llandeilian       Llandeilian     466.0    460.9
    ## 4766       33669        Gisbornian        Gisbornian     460.9    456.1
    ## 4783       33669         Eastonian         Eastonian     456.1    449.5
    ## 4784       33669         Eastonian         Eastonian     456.1    449.5
    ## 4785       33669         Eastonian         Eastonian     456.1    449.5
    ## 4786       33669         Eastonian         Eastonian     456.1    449.5
    ## 4930       33669        Ashgillian        Ashgillian     449.5    443.7
    ## 4931       33669        Ashgillian        Ashgillian     449.5    443.7
    ## 4932       33669        Ashgillian        Ashgillian     449.5    443.7
    ## 4933       33669        Ashgillian        Ashgillian     449.5    443.7
    ## 4934       33669        Ashgillian        Ashgillian     449.5    443.7
    ## 4935       33669        Ashgillian        Ashgillian     449.5    443.7
    ## 4965       33669          Aeronian          Aeronian     440.8    438.5
    ## 4998       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5136       33669        Llandovery        Llandovery     443.4    433.4
    ## 5137       33669        Llandovery        Llandovery     443.4    433.4
    ## 5138       33669        Llandovery        Llandovery     443.4    433.4
    ## 5139       33669        Llandovery        Llandovery     443.4    433.4
    ## 5156       33669        Llandovery        Llandovery     443.4    433.4
    ## 5157       33669        Llandovery        Llandovery     443.4    433.4
    ## 5158       33669        Llandovery        Llandovery     443.4    433.4
    ## 5169       33669        Llandovery        Llandovery     443.4    433.4
    ## 5179       33669        Llandovery        Llandovery     443.4    433.4
    ## 5180       33669        Llandovery        Llandovery     443.4    433.4
    ## 5181       33669        Llandovery        Llandovery     443.4    433.4
    ## 5198       33669        Llandovery        Llandovery     443.4    433.4
    ## 5339       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5372       33669          Aeronian          Aeronian     440.8    438.5
    ## 5813       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5829       33669        Rhuddanian        Rhuddanian     443.4    440.8
    ## 5833       33669        Hirnantian        Hirnantian     445.2    443.4
    ##      reference_no  primary_name primary_reso       subgenus_name
    ## 33             13 Glyptograptus         <NA>                <NA>
    ## 49             13 Glyptograptus         <NA>                <NA>
    ## 51             13 Glyptograptus         <NA>                <NA>
    ## 62             13 Glyptograptus         <NA>                <NA>
    ## 80             13 Glyptograptus         <NA>                <NA>
    ## 165            13 Glyptograptus         <NA>                <NA>
    ## 197            13 Glyptograptus         <NA>                <NA>
    ## 211            78 Glyptograptus         <NA>                <NA>
    ## 225           128 Monograptidae         <NA>                <NA>
    ## 230            87 Glyptograptus         <NA>                <NA>
    ## 238           185 Glyptograptus         <NA>                <NA>
    ## 241           185 Glyptograptus         <NA>                <NA>
    ## 245           185 Glyptograptus         <NA>                <NA>
    ## 255           100 Glyptograptus         <NA>                <NA>
    ## 278           104 Glyptograptus         <NA>                <NA>
    ## 285           104 Glyptograptus         <NA>                <NA>
    ## 289           108 Glyptograptus         <NA>                <NA>
    ## 295           106 Glyptograptus         <NA>                <NA>
    ## 307           107 Glyptograptus         <NA>                <NA>
    ## 316           116 Glyptograptus         <NA>                <NA>
    ## 325           114 Glyptograptus         <NA>                <NA>
    ## 333           114 Glyptograptus         <NA>                <NA>
    ## 360           120 Glyptograptus         <NA>                <NA>
    ## 408           227 Glyptograptus         <NA>                <NA>
    ## 413           227 Glyptograptus         <NA>                <NA>
    ## 417           227 Glyptograptus         <NA>                <NA>
    ## 424           227 Glyptograptus         <NA>                <NA>
    ## 426           227 Glyptograptus         <NA>                <NA>
    ## 427           229 Glyptograptus         <NA>                <NA>
    ## 428           227 Glyptograptus         <NA>                <NA>
    ## 440           437 Glyptograptus         <NA>                <NA>
    ## 448           107 Glyptograptus         <NA>                <NA>
    ## 476           285 Glyptograptus         <NA>                <NA>
    ## 484           285 Glyptograptus         <NA>                <NA>
    ## 492           285 Glyptograptus         <NA>                <NA>
    ## 498           285 Glyptograptus         <NA>                <NA>
    ## 513           286 Glyptograptus         <NA>                <NA>
    ## 531           286 Glyptograptus         <NA>                <NA>
    ## 536           286 Glyptograptus         <NA>                <NA>
    ## 548           286 Glyptograptus         <NA>                <NA>
    ## 550           286 Glyptograptus         <NA>                <NA>
    ## 552           286 Glyptograptus         <NA>                <NA>
    ## 556           286 Glyptograptus         <NA>                <NA>
    ## 584           287 Glyptograptus         <NA>                <NA>
    ## 592           287 Glyptograptus         <NA>                <NA>
    ## 597           287 Glyptograptus         <NA>                <NA>
    ## 636           288 Glyptograptus         <NA>                <NA>
    ## 645           288 Glyptograptus         <NA>                <NA>
    ## 647           288 Glyptograptus         <NA>                <NA>
    ## 673           288 Glyptograptus         <NA>                <NA>
    ## 676           288 Glyptograptus         <NA>                <NA>
    ## 679           288 Glyptograptus         <NA>                <NA>
    ## 695           288 Glyptograptus         <NA>                <NA>
    ## 700           288 Glyptograptus         <NA>                <NA>
    ## 707           288 Glyptograptus         <NA>                <NA>
    ## 726           288 Glyptograptus         <NA>                <NA>
    ## 749           288 Glyptograptus         <NA>                <NA>
    ## 752           288 Glyptograptus         <NA>                <NA>
    ## 779           288 Glyptograptus         <NA>                <NA>
    ## 800           475 Glyptograptus         <NA>                <NA>
    ## 815           475 Glyptograptus         <NA>                <NA>
    ## 817           475 Glyptograptus         <NA>                <NA>
    ## 829           485 Glyptograptus         <NA>                <NA>
    ## 844           485 Glyptograptus         <NA>                <NA>
    ## 845           485 Glyptograptus         <NA>                <NA>
    ## 859           485 Glyptograptus         <NA>                <NA>
    ## 867           485 Glyptograptus         <NA>                <NA>
    ## 895           476 Glyptograptus         <NA>                <NA>
    ## 905           476 Glyptograptus         <NA>                <NA>
    ## 939           476 Glyptograptus         <NA>                <NA>
    ## 951           477 Glyptograptus         <NA>                <NA>
    ## 970           477 Glyptograptus         <NA>                <NA>
    ## 979           477 Glyptograptus         <NA>                <NA>
    ## 1005          479 Glyptograptus         <NA>                <NA>
    ## 1015          479 Glyptograptus         <NA>                <NA>
    ## 1022          479 Glyptograptus         <NA>                <NA>
    ## 1038          479 Glyptograptus         <NA>                <NA>
    ## 1045          479 Glyptograptus         <NA>                <NA>
    ## 1061          479 Glyptograptus         <NA>                <NA>
    ## 1073          479 Glyptograptus         <NA>                <NA>
    ## 1096          480 Glyptograptus         <NA>                <NA>
    ## 1111          480 Glyptograptus         <NA>                <NA>
    ## 1144          480 Glyptograptus         <NA>                <NA>
    ## 1153          480 Glyptograptus         <NA>                <NA>
    ## 1178          480 Glyptograptus         <NA>                <NA>
    ## 1184          480 Glyptograptus         <NA>                <NA>
    ## 1188          480 Glyptograptus         <NA>                <NA>
    ## 1195          480 Glyptograptus         <NA>                <NA>
    ## 1202          480 Glyptograptus         <NA>                <NA>
    ## 1207          480 Glyptograptus         <NA>                <NA>
    ## 1239          480 Glyptograptus         <NA>                <NA>
    ## 1256          481 Glyptograptus         <NA>                <NA>
    ## 1262          481 Glyptograptus         <NA>                <NA>
    ## 1275          481 Glyptograptus         <NA>                <NA>
    ## 1294          483 Glyptograptus         <NA>                <NA>
    ## 1297          483 Glyptograptus         <NA>                <NA>
    ## 1329          613 Glyptograptus         <NA>                <NA>
    ## 1341          648 Glyptograptus         <NA>                <NA>
    ## 1365          631 Glyptograptus         <NA>                <NA>
    ## 1388          664 Glyptograptus         <NA>                <NA>
    ## 1409          622 Glyptograptus         <NA>                <NA>
    ## 1418          607 Glyptograptus            "                <NA>
    ## 1426          670 Glyptograptus         <NA>                <NA>
    ## 1438          667 Glyptograptus         <NA>                <NA>
    ## 1443          632 Glyptograptus         <NA>                <NA>
    ## 1474          608 Glyptograptus         <NA>                <NA>
    ## 1476          603 Glyptograptus         <NA>                <NA>
    ## 1594         6142 Glyptograptus         <NA>                <NA>
    ## 1607         6142 Glyptograptus         <NA>                <NA>
    ## 1614         6142 Glyptograptus         <NA>                <NA>
    ## 1664         6142 Glyptograptus         <NA>                <NA>
    ## 2131          524 Glyptograptus         <NA>                <NA>
    ## 2145          523 Glyptograptus         <NA>                <NA>
    ## 2154          523 Glyptograptus         <NA>                <NA>
    ## 2163          523 Glyptograptus         <NA>                <NA>
    ## 2167          526 Glyptograptus         <NA>                <NA>
    ## 2178          526 Glyptograptus         <NA>                <NA>
    ## 2187          526 Glyptograptus         <NA>                <NA>
    ## 2193          526 Glyptograptus         <NA>                <NA>
    ## 2197          526 Glyptograptus         <NA>                <NA>
    ## 2217          526 Glyptograptus         <NA>                <NA>
    ## 2236          526 Glyptograptus         <NA>                <NA>
    ## 2242          526 Glyptograptus         <NA>                <NA>
    ## 2249          526 Glyptograptus         <NA>                <NA>
    ## 2259          526 Glyptograptus         <NA>                <NA>
    ## 2287         3860 Glyptograptus         <NA>                <NA>
    ## 2340         3862 Glyptograptus         <NA>                <NA>
    ## 2343         3862 Glyptograptus         <NA>                <NA>
    ## 2355         3862 Glyptograptus         <NA>                <NA>
    ## 2360         3862 Glyptograptus         <NA>                <NA>
    ## 2367         3862 Glyptograptus         <NA>                <NA>
    ## 2370         3864 Glyptograptus         <NA>                <NA>
    ## 2382         3864 Glyptograptus         <NA>                <NA>
    ## 2415         6890 Glyptograptus         <NA>                <NA>
    ## 2417         6900 Glyptograptus         <NA>                <NA>
    ## 2427         6916 Glyptograptus         <NA>                <NA>
    ## 2428         6916 Glyptograptus         <NA>                <NA>
    ## 2429         6916 Glyptograptus         <NA>                <NA>
    ## 2445         6922 Glyptograptus         <NA>                <NA>
    ## 2452         6922 Glyptograptus         <NA>                <NA>
    ## 2454         6922 Glyptograptus         <NA>                <NA>
    ## 2489         6984 Glyptograptus         <NA>                <NA>
    ## 2499         7007 Monograptidae         <NA>                <NA>
    ## 2513         7044 Glyptograptus         <NA>                <NA>
    ## 2515         7044 Glyptograptus         <NA>                <NA>
    ## 2516         7044 Glyptograptus         <NA>                <NA>
    ## 2517         7050 Monograptidae         <NA>                <NA>
    ## 2529         7063 Glyptograptus         <NA>                <NA>
    ## 2538         7064 Glyptograptus         <NA>                <NA>
    ## 2615         7121 Glyptograptus         <NA>                <NA>
    ## 2648         6366 Glyptograptus         <NA>                <NA>
    ## 2655         6366 Glyptograptus         <NA>                <NA>
    ## 2662         6372 Glyptograptus         <NA>                <NA>
    ## 2687         6402 Glyptograptus         <NA>                <NA>
    ## 2690         6382 Glyptograptus         <NA>                <NA>
    ## 2831         4379 Monograptidae         <NA>                <NA>
    ## 2882         7455 Monograptidae         <NA>                <NA>
    ## 2936         7455 Glyptograptus         <NA>                <NA>
    ## 2937         7455 Monograptidae         <NA>                <NA>
    ## 3028         7455 Monograptidae         <NA>                <NA>
    ## 3102         7624 Glyptograptus         <NA>                <NA>
    ## 3106         7624 Glyptograptus         <NA>                <NA>
    ## 3115         7624 Glyptograptus         <NA>                <NA>
    ## 3125         7624 Glyptograptus         <NA>                <NA>
    ## 3201         7624 Glyptograptus         <NA>                <NA>
    ## 3215         7624 Glyptograptus         <NA>                <NA>
    ## 3234         7624 Glyptograptus         <NA>                <NA>
    ## 3235         7624 Glyptograptus         <NA>                <NA>
    ## 3275         7624 Glyptograptus         <NA>                <NA>
    ## 3301         7624 Glyptograptus         <NA>                <NA>
    ## 3305         7624 Glyptograptus         <NA>                <NA>
    ## 3306         7624 Glyptograptus         <NA>                <NA>
    ## 3363         7624 Glyptograptus         <NA>                <NA>
    ## 3364         7624 Glyptograptus         <NA>                <NA>
    ## 3378         7624 Glyptograptus         <NA>                <NA>
    ## 3456        10971 Glyptograptus         <NA> Pseudoglyptograptus
    ## 3457        10971 Glyptograptus         <NA> Pseudoglyptograptus
    ## 3470          526 Glyptograptus         <NA>                <NA>
    ## 3477          526 Glyptograptus         <NA>                <NA>
    ## 3487          526 Glyptograptus         <NA>                <NA>
    ## 3506          526 Glyptograptus         <NA>                <NA>
    ## 3532        12470 Glyptograptus         <NA>                <NA>
    ## 3705        18179 Glyptograptus         <NA>                <NA>
    ## 3845        18179 Glyptograptus         <NA>                <NA>
    ## 3846        18179 Glyptograptus         <NA>                <NA>
    ## 3856        18179 Glyptograptus         <NA>                <NA>
    ## 3868        18428 Glyptograptus         <NA>                <NA>
    ## 3883        18428 Glyptograptus         <NA>                <NA>
    ## 3891        18428 Glyptograptus         <NA>                <NA>
    ## 3916        18428 Glyptograptus         <NA>                <NA>
    ## 3939        18428 Glyptograptus         <NA>                <NA>
    ## 3953        18428 Glyptograptus         <NA>                <NA>
    ## 3976        18428 Glyptograptus         <NA>                <NA>
    ## 3986        18428 Glyptograptus         <NA>                <NA>
    ## 4002        18428 Glyptograptus         <NA>                <NA>
    ## 4043        25447 Glyptograptus         <NA>                <NA>
    ## 4114        26007 Glyptograptus         <NA>                <NA>
    ## 4135          108 Glyptograptus         <NA>                <NA>
    ## 4139          108 Glyptograptus         <NA>                <NA>
    ## 4259        35067 Glyptograptus         <NA>                <NA>
    ## 4260        35067 Glyptograptus         <NA>                <NA>
    ## 4272        35067 Glyptograptus         <NA>                <NA>
    ## 4274        35067 Glyptograptus         <NA>                <NA>
    ## 4324        36540  Diplograptus         <NA>       Glyptograptus
    ## 4364        37212 Glyptograptus         <NA>                <NA>
    ## 4374        37212 Glyptograptus         <NA>                <NA>
    ## 4375        37212 Glyptograptus         <NA>                <NA>
    ## 4390        37212 Glyptograptus         <NA>                <NA>
    ## 4398        37212 Glyptograptus         <NA>                <NA>
    ## 4409        37212 Glyptograptus         <NA>                <NA>
    ## 4420        37212 Glyptograptus         <NA>                <NA>
    ## 4421        37212 Glyptograptus         <NA>                <NA>
    ## 4426        37212 Glyptograptus         <NA>                <NA>
    ## 4430        37212 Glyptograptus         <NA>                <NA>
    ## 4438        37212 Glyptograptus         <NA>                <NA>
    ## 4448        37212 Glyptograptus         <NA>                <NA>
    ## 4454        37212 Glyptograptus         <NA>                <NA>
    ## 4455        37212 Glyptograptus         <NA>                <NA>
    ## 4563        46965 Glyptograptus         <NA>                <NA>
    ## 4584        46965 Glyptograptus         <NA>                <NA>
    ## 4585        46965 Glyptograptus         <NA>                <NA>
    ## 4592        46965 Glyptograptus         <NA>                <NA>
    ## 4593        46965 Glyptograptus         <NA>                <NA>
    ## 4629        46965 Glyptograptus         <NA>                <NA>
    ## 4663        46966 Glyptograptus         <NA>                <NA>
    ## 4674        46966 Glyptograptus         <NA>                <NA>
    ## 4675        46966 Glyptograptus         <NA>                <NA>
    ## 4677        46966 Glyptograptus         <NA>                <NA>
    ## 4687        46966 Glyptograptus         <NA>                <NA>
    ## 4696        46966 Glyptograptus         <NA>                <NA>
    ## 4727        46966 Glyptograptus         <NA>                <NA>
    ## 4749        46966 Glyptograptus         <NA>                <NA>
    ## 4752        46966 Glyptograptus         <NA>                <NA>
    ## 4766        46966 Glyptograptus         <NA>                <NA>
    ## 4783        46966 Glyptograptus         <NA>                <NA>
    ## 4784        46966 Glyptograptus         <NA>                <NA>
    ## 4785        46966 Glyptograptus         <NA>                <NA>
    ## 4786        46966 Glyptograptus         <NA>                <NA>
    ## 4930        46966 Glyptograptus         <NA>                <NA>
    ## 4931        46966 Glyptograptus         <NA>                <NA>
    ## 4932        46966 Glyptograptus         <NA>                <NA>
    ## 4933        46966 Glyptograptus         <NA>                <NA>
    ## 4934        46966 Glyptograptus         <NA>                <NA>
    ## 4935        46966 Glyptograptus         <NA>                <NA>
    ## 4965        46966 Glyptograptus         <NA>                <NA>
    ## 4998        47061 Glyptograptus         <NA>                <NA>
    ## 5136        47076 Glyptograptus         <NA>                <NA>
    ## 5137        47076 Glyptograptus         <NA>                <NA>
    ## 5138        47076 Glyptograptus         <NA>                <NA>
    ## 5139        47076 Glyptograptus         <NA>                <NA>
    ## 5156        47076 Glyptograptus         <NA>                <NA>
    ## 5157        47076 Glyptograptus         <NA>                <NA>
    ## 5158        47076 Glyptograptus         <NA>                <NA>
    ## 5169        47076 Glyptograptus         <NA>                <NA>
    ## 5179        47076 Glyptograptus         <NA>                <NA>
    ## 5180        47076 Glyptograptus         <NA>                <NA>
    ## 5181        47076 Glyptograptus         <NA>                <NA>
    ## 5198        47076 Glyptograptus         <NA>                <NA>
    ## 5339        47103 Glyptograptus         <NA>                <NA>
    ## 5372        47103 Glyptograptus         <NA>                <NA>
    ## 5813        48568 Glyptograptus         <NA>                <NA>
    ## 5829        49297 Glyptograptus         <NA>                <NA>
    ## 5833        49361 Glyptograptus         <NA>                <NA>
    ##      subgenus_reso   species_name species_reso subgenus subgenus_no
    ## 33            <NA>            sp.         <NA>       NA          NA
    ## 49            <NA>            sp.         <NA>       NA          NA
    ## 51            <NA>            sp.         <NA>       NA          NA
    ## 62            <NA>            sp.         <NA>       NA          NA
    ## 80            <NA>            sp.         <NA>       NA          NA
    ## 165           <NA>            sp.         <NA>       NA          NA
    ## 197           <NA>            sp.         <NA>       NA          NA
    ## 211           <NA>            sp.         <NA>       NA          NA
    ## 225           <NA>         indet.         <NA>       NA          NA
    ## 230           <NA>            sp.         <NA>       NA          NA
    ## 238           <NA>     tamariscus         aff.       NA          NA
    ## 241           <NA>     nikolayevi         <NA>       NA          NA
    ## 245           <NA>     tamariscus         aff.       NA          NA
    ## 255           <NA>            sp.         <NA>       NA          NA
    ## 278           <NA>            sp.         <NA>       NA          NA
    ## 285           <NA>            sp.         <NA>       NA          NA
    ## 289           <NA>            sp.         <NA>       NA          NA
    ## 295           <NA>            sp.         <NA>       NA          NA
    ## 307           <NA>            sp.         <NA>       NA          NA
    ## 316           <NA>            sp.         <NA>       NA          NA
    ## 325           <NA>            sp.         <NA>       NA          NA
    ## 333           <NA>            sp.         <NA>       NA          NA
    ## 360           <NA>            sp.         <NA>       NA          NA
    ## 408           <NA>  teretiusculus         <NA>       NA          NA
    ## 413           <NA>            sp.         <NA>       NA          NA
    ## 417           <NA>            sp.         <NA>       NA          NA
    ## 424           <NA>            sp.         <NA>       NA          NA
    ## 426           <NA>            sp.         <NA>       NA          NA
    ## 427           <NA>            sp.         <NA>       NA          NA
    ## 428           <NA>            sp.         <NA>       NA          NA
    ## 440           <NA>  teretiusculus          cf.       NA          NA
    ## 448           <NA>            sp.         <NA>       NA          NA
    ## 476           <NA>            sp.         <NA>       NA          NA
    ## 484           <NA>            sp.         <NA>       NA          NA
    ## 492           <NA>            sp.         <NA>       NA          NA
    ## 498           <NA>            sp.         <NA>       NA          NA
    ## 513           <NA>            sp.         <NA>       NA          NA
    ## 531           <NA>            sp.         <NA>       NA          NA
    ## 536           <NA>            sp.         <NA>       NA          NA
    ## 548           <NA>            sp.         <NA>       NA          NA
    ## 550           <NA>            sp.         <NA>       NA          NA
    ## 552           <NA>            sp.         <NA>       NA          NA
    ## 556           <NA>            sp.         <NA>       NA          NA
    ## 584           <NA>            sp.         <NA>       NA          NA
    ## 592           <NA>            sp.         <NA>       NA          NA
    ## 597           <NA>            sp.         <NA>       NA          NA
    ## 636           <NA>            sp.         <NA>       NA          NA
    ## 645           <NA>            sp.         <NA>       NA          NA
    ## 647           <NA>            sp.         <NA>       NA          NA
    ## 673           <NA>            sp.         <NA>       NA          NA
    ## 676           <NA>            sp.         <NA>       NA          NA
    ## 679           <NA>            sp.         <NA>       NA          NA
    ## 695           <NA>            sp.         <NA>       NA          NA
    ## 700           <NA>            sp.         <NA>       NA          NA
    ## 707           <NA>            sp.         <NA>       NA          NA
    ## 726           <NA>            sp.         <NA>       NA          NA
    ## 749           <NA>            sp.         <NA>       NA          NA
    ## 752           <NA>            sp.         <NA>       NA          NA
    ## 779           <NA>            sp.         <NA>       NA          NA
    ## 800           <NA>            sp.         <NA>       NA          NA
    ## 815           <NA>            sp.         <NA>       NA          NA
    ## 817           <NA>            sp.         <NA>       NA          NA
    ## 829           <NA>            sp.         <NA>       NA          NA
    ## 844           <NA>            sp.         <NA>       NA          NA
    ## 845           <NA>            sp.         <NA>       NA          NA
    ## 859           <NA>            sp.         <NA>       NA          NA
    ## 867           <NA>            sp.         <NA>       NA          NA
    ## 895           <NA>            sp.         <NA>       NA          NA
    ## 905           <NA>            sp.         <NA>       NA          NA
    ## 939           <NA>            sp.         <NA>       NA          NA
    ## 951           <NA>            sp.         <NA>       NA          NA
    ## 970           <NA>            sp.         <NA>       NA          NA
    ## 979           <NA>            sp.         <NA>       NA          NA
    ## 1005          <NA>            sp.         <NA>       NA          NA
    ## 1015          <NA>            sp.         <NA>       NA          NA
    ## 1022          <NA>            sp.         <NA>       NA          NA
    ## 1038          <NA>            sp.         <NA>       NA          NA
    ## 1045          <NA>            sp.         <NA>       NA          NA
    ## 1061          <NA>            sp.         <NA>       NA          NA
    ## 1073          <NA>            sp.         <NA>       NA          NA
    ## 1096          <NA>            sp.         <NA>       NA          NA
    ## 1111          <NA>            sp.         <NA>       NA          NA
    ## 1144          <NA>            sp.         <NA>       NA          NA
    ## 1153          <NA>            sp.         <NA>       NA          NA
    ## 1178          <NA>            sp.         <NA>       NA          NA
    ## 1184          <NA>            sp.         <NA>       NA          NA
    ## 1188          <NA>            sp.         <NA>       NA          NA
    ## 1195          <NA>            sp.         <NA>       NA          NA
    ## 1202          <NA>            sp.         <NA>       NA          NA
    ## 1207          <NA>            sp.         <NA>       NA          NA
    ## 1239          <NA>            sp.         <NA>       NA          NA
    ## 1256          <NA>            sp.         <NA>       NA          NA
    ## 1262          <NA>            sp.         <NA>       NA          NA
    ## 1275          <NA>            sp.         <NA>       NA          NA
    ## 1294          <NA>            sp.         <NA>       NA          NA
    ## 1297          <NA>            sp.         <NA>       NA          NA
    ## 1329          <NA>            sp.         <NA>       NA          NA
    ## 1341          <NA>            sp.         <NA>       NA          NA
    ## 1365          <NA>            sp.         <NA>       NA          NA
    ## 1388          <NA>            sp.         <NA>       NA          NA
    ## 1409          <NA>            sp.         <NA>       NA          NA
    ## 1418          <NA>            sp.         <NA>       NA          NA
    ## 1426          <NA>            sp.         <NA>       NA          NA
    ## 1438          <NA>            sp.         <NA>       NA          NA
    ## 1443          <NA>            sp.         <NA>       NA          NA
    ## 1474          <NA>            sp.         <NA>       NA          NA
    ## 1476          <NA>            sp.         <NA>       NA          NA
    ## 1594          <NA>            sp.         <NA>       NA          NA
    ## 1607          <NA>     tamariscus         <NA>       NA          NA
    ## 1614          <NA>       sinuatus         <NA>       NA          NA
    ## 1664          <NA>        auritus       n. sp.       NA          NA
    ## 2131          <NA>            sp.         <NA>       NA          NA
    ## 2145          <NA>            sp.         <NA>       NA          NA
    ## 2154          <NA>            sp.         <NA>       NA          NA
    ## 2163          <NA>            sp.         <NA>       NA          NA
    ## 2167          <NA>            sp.         <NA>       NA          NA
    ## 2178          <NA>            sp.         <NA>       NA          NA
    ## 2187          <NA>            sp.         <NA>       NA          NA
    ## 2193          <NA>            sp.         <NA>       NA          NA
    ## 2197          <NA>            sp.         <NA>       NA          NA
    ## 2217          <NA>            sp.         <NA>       NA          NA
    ## 2236          <NA>            sp.         <NA>       NA          NA
    ## 2242          <NA>            sp.         <NA>       NA          NA
    ## 2249          <NA>            sp.         <NA>       NA          NA
    ## 2259          <NA>            sp.         <NA>       NA          NA
    ## 2287          <NA>            sp.         <NA>       NA          NA
    ## 2340          <NA>            sp.         <NA>       NA          NA
    ## 2343          <NA>            sp.         <NA>       NA          NA
    ## 2355          <NA>            sp.         <NA>       NA          NA
    ## 2360          <NA>            sp.         <NA>       NA          NA
    ## 2367          <NA>            sp.         <NA>       NA          NA
    ## 2370          <NA>            sp.         <NA>       NA          NA
    ## 2382          <NA>            sp.         <NA>       NA          NA
    ## 2415          <NA>            sp.         <NA>       NA          NA
    ## 2417          <NA>            sp.         <NA>       NA          NA
    ## 2427          <NA>   lorrainensis       ex gr.       NA          NA
    ## 2428          <NA>            sp.         <NA>       NA          NA
    ## 2429          <NA>   lorrainensis       ex gr.       NA          NA
    ## 2445          <NA>   lorrainensis       ex gr.       NA          NA
    ## 2452          <NA>   lorrainensis       ex gr.       NA          NA
    ## 2454          <NA>   lorrainensis       ex gr.       NA          NA
    ## 2489          <NA>     tamariscus         <NA>       NA          NA
    ## 2499          <NA>         indet.         <NA>       NA          NA
    ## 2513          <NA>   lorrainensis          cf.       NA          NA
    ## 2515          <NA>   lorrainensis         <NA>       NA          NA
    ## 2516          <NA>   lorrainensis       ex gr.       NA          NA
    ## 2517          <NA>         indet.         <NA>       NA          NA
    ## 2529          <NA>            sp.         <NA>       NA          NA
    ## 2538          <NA>      euglyphus          cf.       NA          NA
    ## 2615          <NA>            sp.         <NA>       NA          NA
    ## 2648          <NA>            sp.         <NA>       NA          NA
    ## 2655          <NA>            sp.         <NA>       NA          NA
    ## 2662          <NA>            sp.         <NA>       NA          NA
    ## 2687          <NA>            sp.         <NA>       NA          NA
    ## 2690          <NA>            sp.         <NA>       NA          NA
    ## 2831          <NA>         indet.         <NA>       NA          NA
    ## 2882          <NA>         indet.         <NA>       NA          NA
    ## 2936          <NA>     tamariscus         aff.       NA          NA
    ## 2937          <NA>         indet.         <NA>       NA          NA
    ## 3028          <NA>         indet.         <NA>       NA          NA
    ## 3102          <NA>            sp.         <NA>       NA          NA
    ## 3106          <NA>     tamariscus          cf.       NA          NA
    ## 3115          <NA>     tamariscus         aff.       NA          NA
    ## 3125          <NA>     tamariscus          cf.       NA          NA
    ## 3201          <NA>           spp.         <NA>       NA          NA
    ## 3215          <NA>        ultimus         <NA>       NA          NA
    ## 3234          <NA>       insertus         <NA>       NA          NA
    ## 3235          <NA>     tamariscus         <NA>       NA          NA
    ## 3275          <NA>            sp.         <NA>       NA          NA
    ## 3301          <NA>            sp.         <NA>       NA          NA
    ## 3305          <NA>     tamariscus          cf.       NA          NA
    ## 3306          <NA>            sp.         <NA>       NA          NA
    ## 3363          <NA>     tamariscus         <NA>       NA          NA
    ## 3364          <NA>            sp.         <NA>       NA          NA
    ## 3378          <NA>            sp.         <NA>       NA          NA
    ## 3456          <NA>            vas         <NA>       NA          NA
    ## 3457          <NA>            vas         <NA>       NA          NA
    ## 3470          <NA>            sp.         <NA>       NA          NA
    ## 3477          <NA>            sp.         <NA>       NA          NA
    ## 3487          <NA>            sp.         <NA>       NA          NA
    ## 3506          <NA>            sp.         <NA>       NA          NA
    ## 3532          <NA>  teretiusculus         <NA>       NA          NA
    ## 3705          <NA> austrodentatus         <NA>       NA          NA
    ## 3845          <NA>  teretiusculus          cf.       NA          NA
    ## 3846          <NA>            sp.         <NA>       NA          NA
    ## 3856          <NA>  teretiusculus          cf.       NA          NA
    ## 3868          <NA>  teretiusculus         <NA>       NA          NA
    ## 3883          <NA>  teretiusculus          cf.       NA          NA
    ## 3891          <NA>            sp.         <NA>       NA          NA
    ## 3916          <NA>  teretiusculus         <NA>       NA          NA
    ## 3939          <NA>  teretiusculus         <NA>       NA          NA
    ## 3953          <NA>  teretiusculus         <NA>       NA          NA
    ## 3976          <NA>       schaferi         <NA>       NA          NA
    ## 3986          <NA>  teretiusculus          cf.       NA          NA
    ## 4002          <NA>  teretiusculus          cf.       NA          NA
    ## 4043          <NA>            sp.         <NA>       NA          NA
    ## 4114          <NA>  teretiusculus          cf.       NA          NA
    ## 4135          <NA>  teretiusculus          cf.       NA          NA
    ## 4139          <NA>  teretiusculus          cf.       NA          NA
    ## 4259          <NA>       dentatus         <NA>       NA          NA
    ## 4260          <NA>            sp.         <NA>       NA          NA
    ## 4272          <NA>       dentatus          cf.       NA          NA
    ## 4274          <NA>            sp.         <NA>       NA          NA
    ## 4324          <NA>  teretiusculus         <NA>       NA          NA
    ## 4364          <NA>            sp.         <NA>       NA          NA
    ## 4374          <NA>  teretiusculus         <NA>       NA          NA
    ## 4375          <NA>            sp.         <NA>       NA          NA
    ## 4390          <NA>            sp.         <NA>       NA          NA
    ## 4398          <NA>  teretiusculus         <NA>       NA          NA
    ## 4409          <NA>            sp.         <NA>       NA          NA
    ## 4420          <NA>  teretiusculus            ?       NA          NA
    ## 4421          <NA>            sp.         <NA>       NA          NA
    ## 4426          <NA>            sp.         <NA>       NA          NA
    ## 4430          <NA>            sp.         <NA>       NA          NA
    ## 4438          <NA>            sp.         <NA>       NA          NA
    ## 4448          <NA>            sp.         <NA>       NA          NA
    ## 4454          <NA>   teretisculus         <NA>       NA          NA
    ## 4455          <NA>            sp.         <NA>       NA          NA
    ## 4563          <NA>         avitus         <NA>       NA          NA
    ## 4584          <NA>       incertus         aff.       NA          NA
    ## 4585          <NA>       incertus         aff.       NA          NA
    ## 4592          <NA>     tamariscus         <NA>       NA          NA
    ## 4593          <NA>     tamariscus         <NA>       NA          NA
    ## 4629          <NA>         enodis          cf.       NA          NA
    ## 4663          <NA>            sp.         <NA>       NA          NA
    ## 4674          <NA>      euglyphus          cf.       NA          NA
    ## 4675          <NA>  teretiusculus         <NA>       NA          NA
    ## 4677          <NA>  teretiusculus         <NA>       NA          NA
    ## 4687          <NA>      euglyphus          cf.       NA          NA
    ## 4696          <NA>      euglyphus          cf.       NA          NA
    ## 4727          <NA>            sp.          cf.       NA          NA
    ## 4749          <NA>            sp.         <NA>       NA          NA
    ## 4752          <NA>            sp.         <NA>       NA          NA
    ## 4766          <NA>      euglyphus         <NA>       NA          NA
    ## 4783          <NA>      euglyphus          cf.       NA          NA
    ## 4784          <NA>      euglyphus          cf.       NA          NA
    ## 4785          <NA>      euglyphus          cf.       NA          NA
    ## 4786          <NA>            sp.         <NA>       NA          NA
    ## 4930          <NA>          altus         <NA>       NA          NA
    ## 4931          <NA>     tamariscus         <NA>       NA          NA
    ## 4932          <NA>     tamariscus         <NA>       NA          NA
    ## 4933          <NA>  teretiusculus          cf.       NA          NA
    ## 4934          <NA>            sp.         <NA>       NA          NA
    ## 4935          <NA>            sp.         <NA>       NA          NA
    ## 4965          <NA>     tamariscus          cf.       NA          NA
    ## 4998          <NA>     tamariscus         aff.       NA          NA
    ## 5136          <NA>         enodis          cf.       NA          NA
    ## 5137          <NA>         gnomus         <NA>       NA          NA
    ## 5138          <NA>       incertus         <NA>       NA          NA
    ## 5139          <NA>     tamariscus         <NA>       NA          NA
    ## 5156          <NA>     laciniosus         <NA>       NA          NA
    ## 5157          <NA>      lanpherei         <NA>       NA          NA
    ## 5158          <NA>     tamariscus         <NA>       NA          NA
    ## 5169          <NA>     tamariscus          cf.       NA          NA
    ## 5179          <NA>         enodis          cf.       NA          NA
    ## 5180          <NA>     laciniosus         <NA>       NA          NA
    ## 5181          <NA>     tamariscus          cf.       NA          NA
    ## 5198          <NA>     laciniosus         <NA>       NA          NA
    ## 5339          <NA>            sp.         <NA>       NA          NA
    ## 5372          <NA>       incertus          cf.       NA          NA
    ## 5813          <NA>       serratus          cf.       NA          NA
    ## 5829          <NA>     tamariscus         <NA>       NA          NA
    ## 5833          <NA>    lungmaensis         <NA>       NA          NA
    ##              genus genus_no        family family_no       order order_no
    ## 33   Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 49   Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 51   Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 62   Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 80   Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 165  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 197  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 211  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 225           <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 230  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 238  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 241  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 245  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 255  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 278  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 285  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 289  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 295  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 307  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 316  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 325  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 333  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 360  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 408  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 413  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 417  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 424  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 426  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 427  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 428  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 440  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 448  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 476  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 484  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 492  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 498  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 513  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 531  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 536  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 548  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 550  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 552  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 556  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 584  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 592  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 597  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 636  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 645  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 647  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 673  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 676  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 679  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 695  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 700  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 707  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 726  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 749  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 752  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 779  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 800  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 815  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 817  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 829  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 844  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 845  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 859  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 867  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 895  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 905  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 939  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 951  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 970  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 979  Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1005 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1015 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1022 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1038 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1045 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1061 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1073 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1096 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1111 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1144 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1153 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1178 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1184 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1188 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1195 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1202 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1207 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1239 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1256 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1262 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1275 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1294 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1297 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1329 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1341 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1365 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1388 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1409 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1418 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1426 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1438 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1443 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1474 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1476 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1594 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1607 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1614 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 1664 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2131 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2145 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2154 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2163 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2167 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2178 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2187 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2193 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2197 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2217 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2236 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2242 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2249 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2259 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2287 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2340 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2343 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2355 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2360 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2367 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2370 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2382 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2415 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2417 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2427 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2428 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2429 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2445 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2452 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2454 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2489 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2499          <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 2513 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2515 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2516 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2517          <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 2529 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2538 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2615 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2648 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2655 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2662 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2687 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2690 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2831          <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 2882          <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 2936 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 2937          <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 3028          <NA>       NA Monograptidae    306248 Bireclinata   306262
    ## 3102 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3106 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3115 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3125 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3201 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3215 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3234 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3235 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3275 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3301 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3305 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3306 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3363 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3364 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3378 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3456 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3457 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3470 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3477 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3487 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3506 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3532 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3705 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3845 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3846 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3856 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3868 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3883 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3891 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3916 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3939 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3953 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3976 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 3986 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4002 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4043 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4114 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4135 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4139 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4259 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4260 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4272 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4274 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4324 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4364 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4374 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4375 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4390 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4398 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4409 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4420 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4421 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4426 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4430 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4438 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4448 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4454 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4455 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4563 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4584 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4585 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4592 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4593 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4629 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4663 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4674 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4675 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4677 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4687 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4696 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4727 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4749 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4752 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4766 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4783 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4784 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4785 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4786 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4930 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4931 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4932 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4933 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4934 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4935 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4965 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 4998 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5136 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5137 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5138 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5139 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5156 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5157 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5158 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5169 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5179 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5180 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5181 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5198 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5339 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5372 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5813 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5829 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ## 5833 Glyptograptus    33669 Monograptidae    306248 Bireclinata   306262
    ##              class class_no       phylum phylum_no           authorizer
    ## 33   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 49   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 51   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 62   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 80   Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 165  Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 197  Graptolithina    33534 Hemichordata     33518         Sepkoski, J.
    ## 211  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 225  Graptolithina    33534 Hemichordata     33518            Alroy, J.
    ## 230  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 238  Graptolithina    33534 Hemichordata     33518            Alroy, J.
    ## 241  Graptolithina    33534 Hemichordata     33518            Alroy, J.
    ## 245  Graptolithina    33534 Hemichordata     33518            Alroy, J.
    ## 255  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 278  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 285  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 289  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 295  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 307  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 316  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 325  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 333  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 360  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 408  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 413  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 417  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 424  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 426  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 427  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 428  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 440  Graptolithina    33534 Hemichordata     33518            Alroy, J.
    ## 448  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 476  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 484  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 492  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 498  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 513  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 531  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 536  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 548  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 550  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 552  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 556  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 584  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 592  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 597  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 636  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 645  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 647  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 673  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 676  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 679  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 695  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 700  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 707  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 726  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 749  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 752  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 779  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 800  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 815  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 817  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 829  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 844  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 845  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 859  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 867  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 895  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 905  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 939  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 951  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 970  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 979  Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1005 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1015 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1022 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1038 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1045 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1061 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1073 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1096 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1111 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1144 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1153 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1178 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1184 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1188 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1195 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1202 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1207 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1239 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1256 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1262 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1275 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1294 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1297 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1329 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1341 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1365 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1388 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1409 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1418 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1426 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1438 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1443 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1474 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1476 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 1594 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 1607 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 1614 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 1664 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2131 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2145 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2154 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2163 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2167 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2178 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2187 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2193 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2197 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2217 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2236 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2242 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2249 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2259 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2287 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2340 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2343 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2355 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2360 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2367 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2370 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2382 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2415 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2417 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2427 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2428 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2429 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2445 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2452 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2454 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2489 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2499 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2513 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2515 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2516 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2517 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2529 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2538 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2615 Graptolithina    33534 Hemichordata     33518          Holland, S.
    ## 2648 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2655 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2662 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2687 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2690 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 2831 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2882 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2936 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 2937 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3028 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3102 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3106 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3115 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3125 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3201 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3215 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3234 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3235 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3275 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3301 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3305 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3306 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3363 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3364 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3378 Graptolithina    33534 Hemichordata     33518            Foote, M.
    ## 3456 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 3457 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 3470 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3477 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3487 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3506 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 3532 Graptolithina    33534 Hemichordata     33518          Aberhan, M.
    ## 3705 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3845 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3846 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3856 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3868 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3883 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3891 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3916 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3939 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3953 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3976 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 3986 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 4002 Graptolithina    33534 Hemichordata     33518            Hendy, A.
    ## 4043 Graptolithina    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4114 Graptolithina    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4135 Graptolithina    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4139 Graptolithina    33534 Hemichordata     33518 Novack-Gottshall, P.
    ## 4259 Graptolithina    33534 Hemichordata     33518          Hopkins, M.
    ## 4260 Graptolithina    33534 Hemichordata     33518          Hopkins, M.
    ## 4272 Graptolithina    33534 Hemichordata     33518          Hopkins, M.
    ## 4274 Graptolithina    33534 Hemichordata     33518          Hopkins, M.
    ## 4324 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4364 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4374 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4375 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4390 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4398 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4409 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4420 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4421 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4426 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4430 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4438 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4448 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4454 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4455 Graptolithina    33534 Hemichordata     33518           Miller, A.
    ## 4563 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4584 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4585 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4592 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4593 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4629 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4663 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4674 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4675 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4677 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4687 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4696 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4727 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4749 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4752 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4766 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4783 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4784 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4785 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4786 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4930 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4931 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4932 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4933 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4934 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4935 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4965 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 4998 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5136 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5137 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5138 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5139 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5156 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5157 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5158 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5169 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5179 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5180 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5181 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5198 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5339 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5372 Graptolithina    33534 Hemichordata     33518        Kiessling, W.
    ## 5813 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 5829 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ## 5833 Graptolithina    33534 Hemichordata     33518           Wagner, P.
    ##                   enterer             modifier
    ## 33            Sommers, M.              unknown
    ## 49            Sommers, M.              unknown
    ## 51            Sommers, M.              unknown
    ## 62            Sommers, M.              unknown
    ## 80            Sommers, M.              unknown
    ## 165           Sommers, M.              unknown
    ## 197           Sommers, M.              unknown
    ## 211  Novack-Gottshall, P.           Wagner, P.
    ## 225           Sommers, M.              unknown
    ## 230  Novack-Gottshall, P.              unknown
    ## 238           Sommers, M.              unknown
    ## 241           Sommers, M.              unknown
    ## 245           Sommers, M.              unknown
    ## 255  Novack-Gottshall, P.           Wagner, P.
    ## 278  Novack-Gottshall, P.              unknown
    ## 285  Novack-Gottshall, P.              unknown
    ## 289  Novack-Gottshall, P.              unknown
    ## 295  Novack-Gottshall, P.              unknown
    ## 307  Novack-Gottshall, P. Novack-Gottshall, P.
    ## 316  Novack-Gottshall, P.              unknown
    ## 325  Novack-Gottshall, P.              unknown
    ## 333  Novack-Gottshall, P.              unknown
    ## 360  Novack-Gottshall, P.              unknown
    ## 408  Novack-Gottshall, P.              unknown
    ## 413  Novack-Gottshall, P.              unknown
    ## 417  Novack-Gottshall, P.              unknown
    ## 424  Novack-Gottshall, P.              unknown
    ## 426  Novack-Gottshall, P.              unknown
    ## 427  Novack-Gottshall, P.              unknown
    ## 428  Novack-Gottshall, P.              unknown
    ## 440           Sommers, M.          Sommers, M.
    ## 448  Novack-Gottshall, P.              unknown
    ## 476  Novack-Gottshall, P.              unknown
    ## 484  Novack-Gottshall, P.              unknown
    ## 492  Novack-Gottshall, P.              unknown
    ## 498  Novack-Gottshall, P.              unknown
    ## 513  Novack-Gottshall, P.              unknown
    ## 531  Novack-Gottshall, P.              unknown
    ## 536  Novack-Gottshall, P.              unknown
    ## 548  Novack-Gottshall, P.              unknown
    ## 550  Novack-Gottshall, P.              unknown
    ## 552  Novack-Gottshall, P.              unknown
    ## 556  Novack-Gottshall, P.              unknown
    ## 584  Novack-Gottshall, P.              unknown
    ## 592  Novack-Gottshall, P.              unknown
    ## 597  Novack-Gottshall, P.              unknown
    ## 636  Novack-Gottshall, P.              unknown
    ## 645  Novack-Gottshall, P.              unknown
    ## 647  Novack-Gottshall, P.              unknown
    ## 673  Novack-Gottshall, P.              unknown
    ## 676  Novack-Gottshall, P.              unknown
    ## 679  Novack-Gottshall, P.              unknown
    ## 695  Novack-Gottshall, P.              unknown
    ## 700  Novack-Gottshall, P.              unknown
    ## 707  Novack-Gottshall, P.              unknown
    ## 726  Novack-Gottshall, P.              unknown
    ## 749  Novack-Gottshall, P.              unknown
    ## 752  Novack-Gottshall, P.              unknown
    ## 779  Novack-Gottshall, P.              unknown
    ## 800  Novack-Gottshall, P.              unknown
    ## 815  Novack-Gottshall, P.              unknown
    ## 817  Novack-Gottshall, P.              unknown
    ## 829  Novack-Gottshall, P.              unknown
    ## 844  Novack-Gottshall, P.              unknown
    ## 845  Novack-Gottshall, P.              unknown
    ## 859  Novack-Gottshall, P.              unknown
    ## 867  Novack-Gottshall, P.              unknown
    ## 895  Novack-Gottshall, P.              unknown
    ## 905  Novack-Gottshall, P.              unknown
    ## 939  Novack-Gottshall, P.              unknown
    ## 951  Novack-Gottshall, P.              unknown
    ## 970  Novack-Gottshall, P.              unknown
    ## 979  Novack-Gottshall, P.              unknown
    ## 1005 Novack-Gottshall, P.              unknown
    ## 1015 Novack-Gottshall, P.              unknown
    ## 1022 Novack-Gottshall, P.              unknown
    ## 1038 Novack-Gottshall, P.              unknown
    ## 1045 Novack-Gottshall, P.              unknown
    ## 1061 Novack-Gottshall, P.              unknown
    ## 1073 Novack-Gottshall, P.              unknown
    ## 1096 Novack-Gottshall, P.              unknown
    ## 1111 Novack-Gottshall, P.              unknown
    ## 1144 Novack-Gottshall, P.              unknown
    ## 1153 Novack-Gottshall, P.              unknown
    ## 1178 Novack-Gottshall, P.              unknown
    ## 1184 Novack-Gottshall, P.              unknown
    ## 1188 Novack-Gottshall, P.              unknown
    ## 1195 Novack-Gottshall, P.              unknown
    ## 1202 Novack-Gottshall, P.              unknown
    ## 1207 Novack-Gottshall, P.              unknown
    ## 1239 Novack-Gottshall, P.              unknown
    ## 1256 Novack-Gottshall, P.              unknown
    ## 1262 Novack-Gottshall, P.              unknown
    ## 1275 Novack-Gottshall, P.              unknown
    ## 1294 Novack-Gottshall, P.              unknown
    ## 1297 Novack-Gottshall, P.              unknown
    ## 1329 Novack-Gottshall, P.              unknown
    ## 1341 Novack-Gottshall, P.              unknown
    ## 1365 Novack-Gottshall, P.              unknown
    ## 1388 Novack-Gottshall, P.              unknown
    ## 1409 Novack-Gottshall, P.              unknown
    ## 1418 Novack-Gottshall, P.              unknown
    ## 1426 Novack-Gottshall, P.              unknown
    ## 1438 Novack-Gottshall, P.              unknown
    ## 1443 Novack-Gottshall, P.              unknown
    ## 1474 Novack-Gottshall, P.              unknown
    ## 1476 Novack-Gottshall, P.              unknown
    ## 1594            Foote, M.              unknown
    ## 1607            Foote, M.              unknown
    ## 1614            Foote, M.              unknown
    ## 1664            Foote, M.              unknown
    ## 2131 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2145 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2154 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2163 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2167 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2178 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2187 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2193 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2197 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2217 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2236 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2242 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2249 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2259 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2287 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2340 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2343 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2355 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2360 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2367 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2370 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2382 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2415           Hanson, T.              unknown
    ## 2417           Hanson, T.              unknown
    ## 2427           Hanson, T.              unknown
    ## 2428           Hanson, T.              unknown
    ## 2429           Hanson, T.              unknown
    ## 2445           Hanson, T.              unknown
    ## 2452           Hanson, T.              unknown
    ## 2454           Hanson, T.              unknown
    ## 2489            Foote, M.              unknown
    ## 2499            Foote, M.              unknown
    ## 2513           Hanson, T.              unknown
    ## 2515           Hanson, T.              unknown
    ## 2516           Hanson, T.              unknown
    ## 2517            Foote, M.              unknown
    ## 2529           Hanson, T.              unknown
    ## 2538           Hanson, T.              unknown
    ## 2615           Hanson, T.              unknown
    ## 2648 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2655 Novack-Gottshall, P.           Wagner, P.
    ## 2662 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2687 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2690 Novack-Gottshall, P. Novack-Gottshall, P.
    ## 2831            Foote, M.              unknown
    ## 2882            Foote, M.              unknown
    ## 2936            Foote, M.              unknown
    ## 2937            Foote, M.              unknown
    ## 3028            Foote, M.              unknown
    ## 3102            Foote, M.              unknown
    ## 3106            Foote, M.              unknown
    ## 3115            Foote, M.              unknown
    ## 3125            Foote, M.              unknown
    ## 3201            Foote, M.              unknown
    ## 3215            Foote, M.              unknown
    ## 3234            Foote, M.              unknown
    ## 3235            Foote, M.              unknown
    ## 3275            Foote, M.              unknown
    ## 3301            Foote, M.              unknown
    ## 3305            Foote, M.              unknown
    ## 3306            Foote, M.              unknown
    ## 3363            Foote, M.              unknown
    ## 3364            Foote, M.              unknown
    ## 3378            Foote, M.              unknown
    ## 3456         Koverman, K.              unknown
    ## 3457         Koverman, K.           Wagner, P.
    ## 3470 Novack-Gottshall, P.              unknown
    ## 3477 Novack-Gottshall, P.              unknown
    ## 3487 Novack-Gottshall, P.              unknown
    ## 3506 Novack-Gottshall, P.              unknown
    ## 3532         Nurnberg, S.              unknown
    ## 3705            Hendy, A.              unknown
    ## 3845            Hendy, A.              unknown
    ## 3846            Hendy, A.              unknown
    ## 3856            Hendy, A.              unknown
    ## 3868            Hendy, A.            Hendy, A.
    ## 3883            Hendy, A.            Hendy, A.
    ## 3891            Hendy, A.              unknown
    ## 3916            Hendy, A.              unknown
    ## 3939            Hendy, A.              unknown
    ## 3953            Hendy, A.              unknown
    ## 3976            Hendy, A.              unknown
    ## 3986            Hendy, A.              unknown
    ## 4002            Hendy, A.              unknown
    ## 4043            Hearn, P.              unknown
    ## 4114            Hearn, P.              unknown
    ## 4135            Hearn, P.              unknown
    ## 4139            Hearn, P.              unknown
    ## 4259          Hopkins, M.              unknown
    ## 4260          Hopkins, M.              unknown
    ## 4272          Hopkins, M.              unknown
    ## 4274          Hopkins, M.              unknown
    ## 4324            Kolbe, S.              unknown
    ## 4364            Kolbe, S.              unknown
    ## 4374            Kolbe, S.              unknown
    ## 4375            Kolbe, S.              unknown
    ## 4390            Kolbe, S.              unknown
    ## 4398            Kolbe, S.              unknown
    ## 4409            Kolbe, S.              unknown
    ## 4420            Kolbe, S.              unknown
    ## 4421            Kolbe, S.              unknown
    ## 4426            Kolbe, S.              unknown
    ## 4430            Kolbe, S.              unknown
    ## 4438            Kolbe, S.              unknown
    ## 4448            Kolbe, S.              unknown
    ## 4454            Kolbe, S.              unknown
    ## 4455            Kolbe, S.              unknown
    ## 4563           Krause, M.           Krause, M.
    ## 4584           Krause, M.           Krause, M.
    ## 4585           Krause, M.           Krause, M.
    ## 4592           Krause, M.           Krause, M.
    ## 4593           Krause, M.           Krause, M.
    ## 4629           Krause, M.           Krause, M.
    ## 4663           Krause, M.              unknown
    ## 4674           Krause, M.              unknown
    ## 4675           Krause, M.              unknown
    ## 4677           Krause, M.              unknown
    ## 4687           Krause, M.              unknown
    ## 4696           Krause, M.           Krause, M.
    ## 4727           Krause, M.              unknown
    ## 4749           Krause, M.              unknown
    ## 4752           Krause, M.              unknown
    ## 4766           Krause, M.              unknown
    ## 4783           Krause, M.              unknown
    ## 4784           Krause, M.           Krause, M.
    ## 4785           Krause, M.           Krause, M.
    ## 4786           Krause, M.           Krause, M.
    ## 4930           Krause, M.           Krause, M.
    ## 4931           Krause, M.           Krause, M.
    ## 4932           Krause, M.           Krause, M.
    ## 4933           Krause, M.           Krause, M.
    ## 4934           Krause, M.           Krause, M.
    ## 4935           Krause, M.           Krause, M.
    ## 4965           Krause, M.           Krause, M.
    ## 4998           Krause, M.           Krause, M.
    ## 5136           Krause, M.              unknown
    ## 5137           Krause, M.              unknown
    ## 5138           Krause, M.              unknown
    ## 5139           Krause, M.              unknown
    ## 5156           Krause, M.              unknown
    ## 5157           Krause, M.              unknown
    ## 5158           Krause, M.              unknown
    ## 5169           Krause, M.              unknown
    ## 5179           Krause, M.              unknown
    ## 5180           Krause, M.              unknown
    ## 5181           Krause, M.              unknown
    ## 5198           Krause, M.              unknown
    ## 5339           Krause, M.              unknown
    ## 5372           Krause, M.              unknown
    ## 5813           Wagner, P.              unknown
    ## 5829           Wagner, P.              unknown
    ## 5833           Wagner, P.              unknown
    ## 
    ## $Nephelograptidae
    ##      occurrence_no record_type reid_no obsolete collection_no
    ## 1517        140480  occurrence      NA       NA         12068
    ##                identified_name identified_rank identified_no
    ## 1517 Ruedemannograptus prantli         species         33811
    ##             taxonomic_reason     accepted_name accepted_rank accepted_no
    ## 1517 taxon not fully entered Ruedemannograptus         genus       33811
    ##      early_interval late_interval early_age late_age reference_no
    ## 1517     Lochkovian    Lochkovian     419.2    410.8         4216
    ##           primary_name primary_reso subgenus_name subgenus_reso
    ## 1517 Ruedemannograptus         <NA>          <NA>          <NA>
    ##      species_name species_reso subgenus subgenus_no             genus
    ## 1517      prantli         <NA>       NA          NA Ruedemannograptus
    ##      genus_no           family family_no      order order_no         class
    ## 1517    33811 Nephelograptidae     88801 Dendroidea    33535 Graptolithina
    ##      class_no       phylum phylum_no authorizer   enterer modifier
    ## 1517    33534 Hemichordata     33518 Miller, A. Sessa, J.  unknown

    # PLot species occurrences
    plotOccData(occSpecies, groupLabel="Species")

![](classwork-Thursday-3-9_files/figure-markdown_strict/unnamed-chunk-2-1.png)

    # Now we look at diversity through time for various ranks
    # convert occurrence data to "timelist" format
    graptTimeSpecies <- occData2timeList(occList = occSpecies)
    graptTimeGenus <- occData2timeList(occList = occGenera)
    graptTimeFamily <- occData2timeList(occList = occFamily)

    head(graptTimeSpecies)

    ## $intTimes
    ##       startTime endTime
    ##  [1,]     488.3   477.7
    ##  [2,]     485.4   477.7
    ##  [3,]     485.4   471.8
    ##  [4,]     478.6   466.0
    ##  [5,]     472.0   468.9
    ##  [6,]     471.8   460.9
    ##  [7,]     471.8   458.4
    ##  [8,]     468.9   466.0
    ##  [9,]     467.3   458.4
    ## [10,]     460.9   456.1
    ## [11,]     460.9   449.5
    ## [12,]     458.4   453.0
    ## [13,]     458.4   443.4
    ## [14,]     457.5   452.0
    ## [15,]     456.1   443.4
    ## [16,]     455.8   445.6
    ## [17,]     453.0   445.6
    ## [18,]     453.0   445.2
    ## [19,]     449.5   443.7
    ## [20,]     445.2   443.4
    ## [21,]     443.4   440.8
    ## [22,]     443.4   433.4
    ## [23,]     440.8   433.4
    ## 
    ## $taxonTimes
    ##                              firstInt lastInt
    ## Adelograptus antiquus               1       3
    ## Adelograptus clarki                 2       2
    ## Amplexograptus rugosus             14      14
    ## Azygograptus novozealandicus        9      10
    ## Climacograptus bicornis            10      15
    ## Climacograptus scalaris            19      23
    ## Corynoides incurvus                14      14
    ## Corynoides tricornis               10      11
    ## Cryptograptus schaferi              7      11
    ## Cryptograptus tricornis             6      13
    ## Dicellograptus anceps              16      19
    ## Dicellograptus complanatus         17      19
    ## Dicellograptus ornatus             18      20
    ## Dicranograptus ramosus             12      12
    ## Dictyonema pulchellum               2       2
    ## Didymograptus nicholsoni            4       9
    ## Diplograptus hughesi               21      23
    ## Geniculograptus pygmaeus           11      19
    ## Goniograptus macer                  5       8
    ## Goniograptus speciosus              8       8
    ## Metabolograptus persculptus        19      21
    ## Normalograptus normalis            19      22
    ## Parabrograptus tribrachiatus       11      11
    ## Pleurograptus linearis             19      19
    ## Pleurograptus lui                  18      19
    ## Pterograptus elegans                9       9
    ## Rhaphidograptus toernquisti        21      23
    ## Tetragraptus insuetus               9       9

    # plot diversity
    pdf(file = "dtt.pdf") # redirect file to a new file
    taxicDivDisc(graptTimeSpecies)
    dev.off() # after this point the plots will go to the plot window instead of PDF

    ## png 
    ##   2

    # Here data are sorted by age. We would like the chart above to look like this chart.
