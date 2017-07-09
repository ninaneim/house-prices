# house-prices
analysis which aims to predict the final price of houses.
the analysis will be done via R

# import data into R
library(readr)
train <- read_csv("~/Desktop/kaggle competition R/train.csv")

# summary train data
summary(train)
       Id           MSSubClass      MSZoning          LotFrontage        LotArea          Street         
 Min.   :   1.0   Min.   : 20.0   Length:1460        Min.   : 21.00   Min.   :  1300   Length:1460       
 1st Qu.: 365.8   1st Qu.: 20.0   Class :character   1st Qu.: 59.00   1st Qu.:  7554   Class :character  
 Median : 730.5   Median : 50.0   Mode  :character   Median : 69.00   Median :  9478   Mode  :character  
 Mean   : 730.5   Mean   : 56.9                      Mean   : 70.05   Mean   : 10517                     
 3rd Qu.:1095.2   3rd Qu.: 70.0                      3rd Qu.: 80.00   3rd Qu.: 11602                     
 Max.   :1460.0   Max.   :190.0                      Max.   :313.00   Max.   :215245                     
                                                     NA's   :259                                         
  
  Alley             LotShape         LandContour         Utilities          LotConfig        
 Length:1460        Length:1460        Length:1460        Length:1460        Length:1460       
 Class :character   Class :character   Class :character   Class :character   Class :character  
 Mode  :character   Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                                               
                                                                                                                                                                                                                                                                                        
  LandSlope         Neighborhood        Condition1         Condition2          BldgType        
 Length:1460        Length:1460        Length:1460        Length:1460        Length:1460       
 Class :character   Class :character   Class :character   Class :character   Class :character  
 Mode  :character   Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                                                                                                                                              
                                                                                                                                                                                              
  HouseStyle         OverallQual      OverallCond      YearBuilt     YearRemodAdd   RoofStyle        
 Length:1460        Min.   : 1.000   Min.   :1.000   Min.   :1872   Min.   :1950   Length:1460       
 Class :character   1st Qu.: 5.000   1st Qu.:5.000   1st Qu.:1954   1st Qu.:1967   Class :character  
 Mode  :character   Median : 6.000   Median :5.000   Median :1973   Median :1994   Mode  :character  
                    Mean   : 6.099   Mean   :5.575   Mean   :1971   Mean   :1985                     
                    3rd Qu.: 7.000   3rd Qu.:6.000   3rd Qu.:2000   3rd Qu.:2004                     
                    Max.   :10.000   Max.   :9.000   Max.   :2010   Max.   :2010                     
                                                                                                     
   RoofMatl         Exterior1st        Exterior2nd         MasVnrType          MasVnrArea      ExterQual        
 Length:1460        Length:1460        Length:1460        Length:1460        Min.   :   0.0   Length:1460       
 Class :character   Class :character   Class :character   Class :character   1st Qu.:   0.0   Class :character  
 Mode  :character   Mode  :character   Mode  :character   Mode  :character   Median :   0.0   Mode  :character  
                                                                             Mean   : 103.7                     
                                                                             3rd Qu.: 166.0                     
                                                                             Max.   :1600.0                     
                                                                             NA's   :8                          

ExterCond          Foundation          BsmtQual           BsmtCond         BsmtExposure      
 Length:1460        Length:1460        Length:1460        Length:1460        Length:1460       
 Class :character   Class :character   Class :character   Class :character   Class :character  
 Mode  :character   Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                                               
                                                                                                                                                                                                                                                                                             
 BsmtFinType1         BsmtFinSF1     BsmtFinType2         BsmtFinSF2        BsmtUnfSF       TotalBsmtSF    
 Length:1460        Min.   :   0.0   Length:1460        Min.   :   0.00   Min.   :   0.0   Min.   :   0.0  
 Class :character   1st Qu.:   0.0   Class :character   1st Qu.:   0.00   1st Qu.: 223.0   1st Qu.: 795.8  
 Mode  :character   Median : 383.5   Mode  :character   Median :   0.00   Median : 477.5   Median : 991.5  
                    Mean   : 443.6                      Mean   :  46.55   Mean   : 567.2   Mean   :1057.4  
                    3rd Qu.: 712.2                      3rd Qu.:   0.00   3rd Qu.: 808.0   3rd Qu.:1298.2  
                    Max.   :5644.0                      Max.   :1474.00   Max.   :2336.0   Max.   :6110.0  
                                                                                                           
   Heating           HeatingQC          CentralAir         Electrical           1stFlrSF       2ndFlrSF   
 Length:1460        Length:1460        Length:1460        Length:1460        Min.   : 334   Min.   :   0  
 Class :character   Class :character   Class :character   Class :character   1st Qu.: 882   1st Qu.:   0  
 Mode  :character   Mode  :character   Mode  :character   Mode  :character   Median :1087   Median :   0  
                                                                             Mean   :1163   Mean   : 347  
                                                                             3rd Qu.:1391   3rd Qu.: 728  
                                                                             Max.   :4692   Max.   :2065  
                                                                                                          
  LowQualFinSF       GrLivArea     BsmtFullBath     BsmtHalfBath        FullBath        HalfBath     
 Min.   :  0.000   Min.   : 334   Min.   :0.0000   Min.   :0.00000   Min.   :0.000   Min.   :0.0000  
 1st Qu.:  0.000   1st Qu.:1130   1st Qu.:0.0000   1st Qu.:0.00000   1st Qu.:1.000   1st Qu.:0.0000  
 Median :  0.000   Median :1464   Median :0.0000   Median :0.00000   Median :2.000   Median :0.0000  
 Mean   :  5.845   Mean   :1515   Mean   :0.4253   Mean   :0.05753   Mean   :1.565   Mean   :0.3829  
 3rd Qu.:  0.000   3rd Qu.:1777   3rd Qu.:1.0000   3rd Qu.:0.00000   3rd Qu.:2.000   3rd Qu.:1.0000  
 Max.   :572.000   Max.   :5642   Max.   :3.0000   Max.   :2.00000   Max.   :3.000   Max.   :2.0000  
                                                                                                     
  BedroomAbvGr    KitchenAbvGr   KitchenQual         TotRmsAbvGrd     Functional          Fireplaces   
 Min.   :0.000   Min.   :0.000   Length:1460        Min.   : 2.000   Length:1460        Min.   :0.000  
 1st Qu.:2.000   1st Qu.:1.000   Class :character   1st Qu.: 5.000   Class :character   1st Qu.:0.000  
 Median :3.000   Median :1.000   Mode  :character   Median : 6.000   Mode  :character   Median :1.000  
 Mean   :2.866   Mean   :1.047                      Mean   : 6.518                      Mean   :0.613  
 3rd Qu.:3.000   3rd Qu.:1.000                      3rd Qu.: 7.000                      3rd Qu.:1.000  
 Max.   :8.000   Max.   :3.000                      Max.   :14.000                      Max.   :3.000  
                                                                                                       
 FireplaceQu         GarageType         GarageYrBlt   GarageFinish         GarageCars      GarageArea    
 Length:1460        Length:1460        Min.   :1900   Length:1460        Min.   :0.000   Min.   :   0.0  
 Class :character   Class :character   1st Qu.:1961   Class :character   1st Qu.:1.000   1st Qu.: 334.5  
 Mode  :character   Mode  :character   Median :1980   Mode  :character   Median :2.000   Median : 480.0  
                                       Mean   :1979                      Mean   :1.767   Mean   : 473.0  
                                       3rd Qu.:2002                      3rd Qu.:2.000   3rd Qu.: 576.0  
                                       Max.   :2010                      Max.   :4.000   Max.   :1418.0  
                                       NA's   :81                                                        
 
 GarageQual         GarageCond         PavedDrive          WoodDeckSF      OpenPorchSF     EnclosedPorch   
 Length:1460        Length:1460        Length:1460        Min.   :  0.00   Min.   :  0.00   Min.   :  0.00  
 Class :character   Class :character   Class :character   1st Qu.:  0.00   1st Qu.:  0.00   1st Qu.:  0.00  
 Mode  :character   Mode  :character   Mode  :character   Median :  0.00   Median : 25.00   Median :  0.00  
                                                          Mean   : 94.24   Mean   : 46.66   Mean   : 21.95  
                                                          3rd Qu.:168.00   3rd Qu.: 68.00   3rd Qu.:  0.00  
                                                          Max.   :857.00   Max.   :547.00   Max.   :552.00  
                                                                                                            
   3SsnPorch       ScreenPorch        PoolArea          PoolQC             Fence           MiscFeature       
 Min.   :  0.00   Min.   :  0.00   Min.   :  0.000   Length:1460        Length:1460        Length:1460       
 1st Qu.:  0.00   1st Qu.:  0.00   1st Qu.:  0.000   Class :character   Class :character   Class :character  
 Median :  0.00   Median :  0.00   Median :  0.000   Mode  :character   Mode  :character   Mode  :character  
 Mean   :  3.41   Mean   : 15.06   Mean   :  2.759                                                           
 3rd Qu.:  0.00   3rd Qu.:  0.00   3rd Qu.:  0.000                                                           
 Max.   :508.00   Max.   :480.00   Max.   :738.000                                                           
                                                                                                             
    MiscVal             MoSold           YrSold       SaleType         SaleCondition        SalePrice     
 Min.   :    0.00   Min.   : 1.000   Min.   :2006   Length:1460        Length:1460        Min.   : 34900  
 1st Qu.:    0.00   1st Qu.: 5.000   1st Qu.:2007   Class :character   Class :character   1st Qu.:129975  
 Median :    0.00   Median : 6.000   Median :2008   Mode  :character   Mode  :character   Median :163000  
 Mean   :   43.49   Mean   : 6.322   Mean   :2008                                         Mean   :180921  
 3rd Qu.:    0.00   3rd Qu.: 8.000   3rd Qu.:2009                                         3rd Qu.:214000  
 Max.   :15500.00   Max.   :12.000   Max.   :2010                                         Max.   :755000  
