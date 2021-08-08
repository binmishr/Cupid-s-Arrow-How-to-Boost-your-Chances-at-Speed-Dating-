# Cupid-s-Arrow-How-to-Boost-your-Chances-at-Speed-Dating

The dataset comprises the following 18 feature variables…

    LikeM How much the male likes his partner (1-10 scale)
    LikeF How much the female likes her partner (1-10 scale)
    PartnerYesM Male’s estimate of chance the female wants another date (1-10 scale)
    PartnerYesF Female’s estimate of chance the male wants another date (1-10 scale)
    AgeM Male’s age (in years)
    AgeF Females age (in years)
    RaceM Male’s race: Asian, Black, Caucasian, Latino, or Other
    RaceF Female’s race: Asian, Black, Caucasian, Latino, or Other
    AttractiveM Male’s rating of female’s attractiveness (1-10 scale)
    AttractiveF Female’s rating of male’s attractiveness (1-10 scale)
    SincereM Male’s rating of female’s sincerity (1-10 scale)
    SincereF Female’s rating of male’s sincerity (1-10 scale)
    IntelligentM Male’s rating of female’s intelligence (1-10 scale)
    IntelligentF Female’s rating of male’s intelligence (1-10 scale)
    FunM Male’s rating of female as fun (1-10 scale)
    FunF Female’s rating of male as fun (1-10 scale)
    AmbitiousM Male’s rating of female’s ambition (1-10 scale)
    AmbitiousF Female’s rating of male’s ambition (1-10 scale)
    SharedInterestsM Male’s rating of female’s shared interests (1-10 scale)
    SharedInterestsF Female’s rating of male’s shared interests (1-10 scale)

…and 2 target variables:

    DecisionMale Would the male like another date? Yes or No
    DecisionFemale Would the female like another date? Yes or No

Without further ado let us fire up our by now well known OneR package (on CRAN) to get right into the matter:

library(OneR)
library(Lock5withR)
data("SpeedDating")
data <- SpeedDating[-c(1, 2)]
OneR(optbin(DecisionMale ~., data = data, method = "infogain"), verbose = TRUE)
## Warning in optbin.data.frame(x = data, method = method, na.omit = na.omit): 76
## instance(s) removed due to missing values
## Warning in OneR.data.frame(optbin(DecisionMale ~ ., data = data, method =
## "infogain"), : data contains unused factor levels
## 
##     Attribute        Accuracy
## 1 * AttractiveM      78%     
## 2   LikeM            72%     
## 3   PartnerYesM      64%     
## 4   SharedInterestsM 63%     
## 5   FunM             60.5%   
## 6   AmbitiousM       59%     
## 7   PartnerYesF      58.5%   
## 8   AgeM             57%     
## 8   RaceF            57%     
## 10  AttractiveF      56.5%   
## 10  IntelligentM     56.5%   
## 12  IntelligentF     56%     
## 13  AmbitiousF       55.5%   
## 14  AgeF             55%     
## 14  RaceM            55%     
## 14  FunF             55%     
## 17  LikeF            54.5%   
## 17  SincereM         54.5%   
## 17  SincereF         54.5%   
## 17  SharedInterestsF 54.5%   
## 17  DecisionFemale   54.5%   
## ---
## Chosen attribute due to accuracy
## and ties method (if applicable): '*'
## 
## Call:
## OneR.data.frame(x = optbin(DecisionMale ~ ., data = data, method = "infogain"), 
##     verbose = TRUE)
## 
## Rules:
## If AttractiveM = (1.99,6] then DecisionMale = No
## If AttractiveM = (6,10]   then DecisionMale = Yes
## 
## Accuracy:
## 156 of 200 instances classified correctly (78%)

We can see that when it comes to men attractiveness is the main predictor. It is even more important than how much he likes her, which comes in second place. The third feature (PartnerYesM Male’s estimate of chance the female wants another date) is particularly interesting:

OneR(optbin(DecisionMale ~ PartnerYesM, data = data, method = "infogain"))
## Warning in optbin.data.frame(x = data, method = method, na.omit = na.omit): 4
## instance(s) removed due to missing values
## 
## Call:
## OneR.data.frame(x = optbin(DecisionMale ~ PartnerYesM, data = data, 
##     method = "infogain"))
## 
## Rules:
## If PartnerYesM = (-0.01,5] then DecisionMale = No
## If PartnerYesM = (5,10]    then DecisionMale = Yes
## 
## Accuracy:
## 180 of 272 instances classified correctly (66.18%)

It shows that even his expectation of the woman wanting another date with him leads to him wanting another date with her! If you show interest in a potential partner this interest will be reciprocated!

All the other features like intelligence, sincerity, fun, shared interests but also age and race are not very good at predicting the outcome of the date.

Ok, in a way this didn’t come as a surprise, everybody knows that men are superficial beings who only look at the outer qualities of a woman. Surely women will look more at inner values, like intelligence, sincerity, or at least shared interests, right? Let’s have a look:

OneR(optbin(DecisionFemale ~., data = data, method = "infogain"), verbose = TRUE)
## Warning in optbin.data.frame(x = data, method = method, na.omit = na.omit): 76
## instance(s) removed due to missing values
## Warning in OneR.data.frame(optbin(DecisionFemale ~ ., data = data, method =
## "infogain"), : data contains unused factor levels
## 
##     Attribute        Accuracy
## 1 * AttractiveF      73.5%   
## 2   LikeF            68.5%   
## 2   FunF             68.5%   
## 4   PartnerYesF      66.5%   
## 5   SharedInterestsF 66%     
## 6   PartnerYesM      62.5%   
## 7   AmbitiousM       61.5%   
## 8   SincereM         59%     
## 8   IntelligentF     59%     
## 10  IntelligentM     58.5%   
## 10  FunM             58.5%   
## 12  LikeM            58%     
## 12  AttractiveM      58%     
## 12  SharedInterestsM 58%     
## 15  AgeF             57.5%   
## 16  RaceF            56%     
## 17  RaceM            55%     
## 18  AgeM             54.5%   
## 18  SincereF         54.5%   
## 18  AmbitiousF       54.5%   
## 18  DecisionMale     54.5%   
## ---
## Chosen attribute due to accuracy
## and ties method (if applicable): '*'
## 
## Call:
## OneR.data.frame(x = optbin(DecisionFemale ~ ., data = data, method = "infogain"), 
##     verbose = TRUE)
## 
## Rules:
## If AttractiveF = (0.991,6] then DecisionFemale = No
## If AttractiveF = (6,10]    then DecisionFemale = Yes
## 
## Accuracy:
## 147 of 200 instances classified correctly (73.5%)

Oh dear, the same result. The most important quality to getting to the next level is yet again the attractiveness and the order of the following features is more or less the same, with the notable exception of FunF Female’s rating of male as fun:

OneR(optbin(DecisionFemale ~ FunF, data = data, method = "infogain"))
## Warning in optbin.data.frame(x = data, method = method, na.omit = na.omit): 6
## instance(s) removed due to missing values
## 
## Call:
## OneR.data.frame(x = optbin(DecisionFemale ~ FunF, data = data, 
##     method = "infogain"))
## 
## Rules:
## If FunF = (0.991,6] then DecisionFemale = No
## If FunF = (6,10]    then DecisionFemale = Yes
## 
## Accuracy:
## 186 of 270 instances classified correctly (68.89%)

So, to summarize: attractiveness is the most important quality, yet you only have limited control over it. But not all is lost if you keep the following in mind: if you are a woman signal that you are interested in the guy, and if you are a guy try to be fun!
