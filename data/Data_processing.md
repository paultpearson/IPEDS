Downloading the 2012 IPEDS data
===============================

2012 IPEDS (final release) data were downloaded from the IPEDS data center website

[http://nces.ed.gov/ipeds/datacenter/CDSPreview.aspx](http://nces.ed.gov/ipeds/datacenter/CDSPreview.aspx)

on June 3, 2014 using the 380 institutions in Minnesota, Wisconsin, Illinois, Indiana, Michigan, and Ohio found in the file

`C:\research\IPEDS\data\DC_InstGroup_62232_upper_midwest.uid`

Here are the download instructions:

1. [http://nces.ed.gov/ipeds/datacenter/Default.aspx](http://nces.ed.gov/ipeds/datacenter/Default.aspx)
2. Click "Download custom data files"
3. Select "Use final release data" (default) and click "Continue"
4. Select institutions by clicking the "Uploading a file" link.
5. Login in.
6. Upload the `DC_InstGroup_62232_upper_midwest.uid` file and click "Submit".
7. In the "Select Variables" tab, click on one of the ten categories of variables.  
8. Click to open all of the subcategories and "select all variables" within each subcategory.
9. When finished with a category, click the "Continue" button near the top of the page.
10. On the results tab, do not impute data, and click the CSV link to get a zip file with CSV data and an HTML codebook.
11. Click "Start Over" and repeat this process on another of the ten categories.

I saved the files in `data/2012/raw/nn_descriptive_name.csv` and similarly for the html codebook files.

Instructions for how to use the IPEDS datacenter can be found at [https://nces.ed.gov/ipeds/datacenter/IPEDSManual.pdf](https://nces.ed.gov/ipeds/datacenter/IPEDSManual.pdf)

----

Processing the 2012 IPEDS Raw Data into Analytic Data
=====================================================

Eventually, this script will load the raw 2012 IPEDS data and process it into a tidy data set suitable for analysis.  Right now, it just loads the data files I downloaded and prints out some information.


Category 1: Frequently used derived variables
---------------------------------------------


```r
df1 <- read.csv("2012/raw/01_Frequently_used_derived_variables.csv")
dim(df1)
```

```
## [1] 380 377
```

```r
names(df1)
```

```
##   [1] "unitid"                                                                                                                                                 
##   [2] "institution.name"                                                                                                                                       
##   [3] "year"                                                                                                                                                   
##   [4] "DRVIC2012.Percent.admitted...total"                                                                                                                     
##   [5] "DRVIC2012.Percent.admitted...men"                                                                                                                       
##   [6] "DRVIC2012.Percent.admitted...women"                                                                                                                     
##   [7] "DRVIC2012.Admissions.yield...total"                                                                                                                     
##   [8] "DRVIC2012.Admissions.yield...men"                                                                                                                       
##   [9] "DRVIC2012.Admissions.yield...women"                                                                                                                     
##  [10] "DRVIC2012.Admissions.yield...full.time"                                                                                                                 
##  [11] "DRVIC2012.Admissions.yield...full.time.men"                                                                                                             
##  [12] "DRVIC2012.Admissions.yield...full.time.women"                                                                                                           
##  [13] "DRVIC2012.Admissions.yield...part.time"                                                                                                                 
##  [14] "DRVIC2012.Admissions.yield...part.time.men"                                                                                                             
##  [15] "DRVIC2012.Admissions.yield...part.time.women"                                                                                                           
##  [16] "DRVIC2012.Tuition.and.fees..2009.10"                                                                                                                    
##  [17] "DRVIC2012.Tuition.and.fees..2010.11"                                                                                                                    
##  [18] "DRVIC2012.Tuition.and.fees..2011.12"                                                                                                                    
##  [19] "DRVIC2012.Tuition.and.fees..2012.13"                                                                                                                    
##  [20] "DRVIC2012.Total.price.for.in.district.students.living.on.campus..2012.13"                                                                               
##  [21] "DRVIC2012.Total.price.for.in.state.students.living.on.campus.2012.13"                                                                                   
##  [22] "DRVIC2012.Total.price.for.out.of.state.students.living.on.campus.2012.13"                                                                               
##  [23] "DRVIC2012.Total.price.for.in.district.students.living.off.campus..not.with.family...2012.13"                                                            
##  [24] "DRVIC2012.Total.price.for.in.state.students.living.off.campus..not.with.family...2012.13"                                                               
##  [25] "DRVIC2012.Total.price.for.out.of.state.students.living.off.campus..not.with.family...2012.13"                                                           
##  [26] "DRVIC2012.Total.price.for.in.district.students.living.off.campus..with.family...2012.13"                                                                
##  [27] "DRVIC2012.Total.price.for.in.state.students.living.off.campus..with.family...2012.13"                                                                   
##  [28] "DRVIC2012.Total.price.for.out.of.state.students.living.off.campus..with.family...2012.13"                                                               
##  [29] "HD2012.Institution.size.category"                                                                                                                       
##  [30] "HD2012.State.abbreviation"                                                                                                                              
##  [31] "HD2012.FIPS.state.code"                                                                                                                                 
##  [32] "HD2012.Geographic.region"                                                                                                                               
##  [33] "HD2012.Sector.of.institution"                                                                                                                           
##  [34] "HD2012.Level.of.institution"                                                                                                                            
##  [35] "HD2012.Control.of.institution"                                                                                                                          
##  [36] "HD2012.Degree.granting.status"                                                                                                                          
##  [37] "HD2012.Historically.Black.College.or.University"                                                                                                        
##  [38] "HD2012.Tribal.college"                                                                                                                                  
##  [39] "HD2012.Degree.of.urbanization..Urban.centric.locale."                                                                                                   
##  [40] "HD2012.Postsecondary.and.Title.IV.institution.indicator"                                                                                                
##  [41] "HD2012.Institutional.category"                                                                                                                          
##  [42] "HD2012.Carnegie.Classification.2010..Basic"                                                                                                             
##  [43] "HD2012.Carnegie.Classification.2010..Undergraduate.Instructional.Program"                                                                               
##  [44] "HD2012.Carnegie.Classification.2010..Graduate.Instructional.Program"                                                                                    
##  [45] "HD2012.Carnegie.Classification.2010..Undergraduate.Profile"                                                                                             
##  [46] "HD2012.Carnegie.Classification.2010..Enrollment.Profile"                                                                                                
##  [47] "HD2012.Carnegie.Classification.2010..Size.and.Setting"                                                                                                  
##  [48] "HD2012.Land.Grant.Institution"                                                                                                                          
##  [49] "HD2012.Carnegie.Classification.2000"                                                                                                                    
##  [50] "HD2012.Data.Feedback.Report.comparison.group.category.created.by.NCES"                                                                                  
##  [51] "HD2012.Data.Feedback.Report...Institution.submitted.a..custom.comparison.group"                                                                         
##  [52] "HD2012.Institution.size.category.1"                                                                                                                     
##  [53] "DRVEF2012.Total..enrollment"                                                                                                                            
##  [54] "DRVEF2012.Full.time.enrollment"                                                                                                                         
##  [55] "DRVEF2012.Part.time.enrollment"                                                                                                                         
##  [56] "DRVEF2012.Full.time.equivalent.fall.enrollment"                                                                                                         
##  [57] "DRVEF2012.Undergraduate.enrollment"                                                                                                                     
##  [58] "DRVEF2012.First.time.degree.certificate.seeking.undergraduate.enrollment"                                                                               
##  [59] "DRVEF2012.Transfer.in.degree.certificate.seeking.undergraduate.enrollment"                                                                              
##  [60] "DRVEF2012.Continuing.degree.certificate.seeking.undergraduate.enrollment"                                                                               
##  [61] "DRVEF2012.Nondegree.certificate.seeking.undergraduate.enrollment"                                                                                       
##  [62] "DRVEF2012.Graduate.enrollment"                                                                                                                          
##  [63] "DRVEF2012.Full.time.undergraduate.enrollment"                                                                                                           
##  [64] "DRVEF2012.Full.time.first.time.degree.certificate.seeking.undergraduate.enrollment"                                                                     
##  [65] "DRVEF2012.Full.time.transfer.in.degree.certificate.seeking.undergraduate.enrollment"                                                                    
##  [66] "DRVEF2012.Full.time.continuing.degree.certificate.seeking.undergraduate.enrollment"                                                                     
##  [67] "DRVEF2012.Full.time.nondegree.certificate.seeking.undergraduate.enrollment"                                                                             
##  [68] "DRVEF2012.Full.time.graduate.enrollment"                                                                                                                
##  [69] "DRVEF2012.Part.time.undergraduate.enrollment"                                                                                                           
##  [70] "DRVEF2012.Part.time.first.time.degree.certificate.seeking.undergraduate.enrollment"                                                                     
##  [71] "DRVEF2012.Part.time.transfer.in.degree.certificate.seeking.undergraduate.enrollment"                                                                    
##  [72] "DRVEF2012.Part.time.continuing.degree.certificate.seeking.undergraduate.enrollment"                                                                     
##  [73] "DRVEF2012.Part.time.nondegree.certificate.seeking.undergraduate.enrollment"                                                                             
##  [74] "DRVEF2012.Part.time.graduate.enrollment"                                                                                                                
##  [75] "DRVEF2012.Percent.of.total.enrollment.that.are.American.Indian.or.Alaska.Native"                                                                        
##  [76] "DRVEF2012.Percent.of.total.enrollment.that.are.Asian"                                                                                                   
##  [77] "DRVEF2012.Percent.of.total.enrollment.that.are.Black.or.African.American"                                                                               
##  [78] "DRVEF2012.Percent.of.total.enrollment.that.are.Hispanic.Latino"                                                                                         
##  [79] "DRVEF2012.Percent.of.total.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander"                                                               
##  [80] "DRVEF2012.Percent.of.total.enrollment.that.are.White"                                                                                                   
##  [81] "DRVEF2012.Percent.of.total.enrollment.that.are.two.or.more.races"                                                                                       
##  [82] "DRVEF2012.Percent.of.total.enrollment.that.are.Race.ethnicity.unknown"                                                                                  
##  [83] "DRVEF2012.Percent.of.total.enrollment.that.are.Nonresident.Alien"                                                                                       
##  [84] "DRVEF2012.Percent.of.total.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander"                                                                  
##  [85] "DRVEF2012.Percent.of.total.enrollment.that.are.women"                                                                                                   
##  [86] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.American.Indian.or.Alaska.Native"                                                                
##  [87] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Asian"                                                                                           
##  [88] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Black.or.African.American"                                                                       
##  [89] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Hispanic.Latino"                                                                                 
##  [90] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander"                                                       
##  [91] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.White"                                                                                           
##  [92] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.two.or.more.races"                                                                               
##  [93] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Race.ethnicity.unknown"                                                                          
##  [94] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Nonresident.Alien"                                                                               
##  [95] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander"                                                          
##  [96] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.women"                                                                                           
##  [97] "DRVEF2012.Percent.of.graduate.enrollment.that.are.American.Indian.or.Alaska.Native"                                                                     
##  [98] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Asian"                                                                                                
##  [99] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Black.or.African.American"                                                                            
## [100] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Hispanic.Latino"                                                                                      
## [101] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander"                                                            
## [102] "DRVEF2012.Percent.of.graduate.enrollment.that.are.White"                                                                                                
## [103] "DRVEF2012.Percent.of.graduate.enrollment.that.are.two.or.more.races"                                                                                    
## [104] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Race.ethnicity.unknown"                                                                               
## [105] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Nonresident.Alien"                                                                                    
## [106] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander"                                                               
## [107] "DRVEF2012.Percent.of.graduate.enrollment.that.are.women"                                                                                                
## [108] "EF2012D.Student.to.faculty.ratio"                                                                                                                       
## [109] "EF2012D.Full.time.retention.rate..2012"                                                                                                                 
## [110] "EF2012D.Part.time.retention.rate..2012"                                                                                                                 
## [111] "DRVEF2012.Full.time..first.time..degree.certificate.seeking.undergraduates..GRS.Cohort..as.percent.of.all.undergraduates"                               
## [112] "EF2012D.Current.year.GRS.cohort.as.a.percent.of.entering.class"                                                                                         
## [113] "DRVEF2012.Adult.age..25.64..enrollment..all.students"                                                                                                   
## [114] "DRVEF2012.Adult.age..25.64..enrollment..undergraduate"                                                                                                  
## [115] "DRVEF2012.Adult.age..25.64..enrollment..graduate"                                                                                                       
## [116] "DRVEF2012.Adult.age..25.64..enrollment..full.time.students"                                                                                             
## [117] "DRVEF2012.Adult.age..25.64..enrollment..full.time.undergraduate"                                                                                        
## [118] "DRVEF2012.Adult.age..25.64..enrollment..full.time.graduate"                                                                                             
## [119] "DRVEF2012.Adult.age..25.64..enrollment..part.time.students"                                                                                             
## [120] "DRVEF2012.Adult.age..25.64..enrollment..part.time.undergraduate"                                                                                        
## [121] "DRVEF2012.Adult.age..25.64..enrollment..part.time.graduate"                                                                                             
## [122] "DRVEF2012.Percent.of.undergraduate.enrollment.under.18"                                                                                                 
## [123] "DRVEF2012.Percent.of.undergraduate.enrollment.18.24"                                                                                                    
## [124] "DRVEF2012.Percent.of.undergraduate.enrollment..25.64"                                                                                                   
## [125] "DRVEF2012.Percent.of.undergraduate.enrollment.over.65"                                                                                                  
## [126] "DRVEF_RM2012.Number.of.first.time.undergraduates...in.state"                                                                                            
## [127] "DRVEF_RM2012.Percent.of.first.time.undergraduates...in.state"                                                                                           
## [128] "DRVEF_RM2012.Number.of.first.time.undergraduates...out.of.state"                                                                                        
## [129] "DRVEF_RM2012.Percent.of.first.time.undergraduates...out.of.state"                                                                                       
## [130] "DRVEF_RM2012.Number.of.first.time.undergraduates...foreign.countries"                                                                                   
## [131] "DRVEF_RM2012.Percent.of.first.time.undergraduates...foreign.countries"                                                                                  
## [132] "DRVEF_RM2012.Number.of.first.time.undergraduates...residence.unknown"                                                                                   
## [133] "DRVEF_RM2012.Percent.of.first.time.undergraduates...residence.unknown"                                                                                  
## [134] "DRVEFDE2012.Percent.of.students.enrolled.exclusively.in.distance.education.courses"                                                                     
## [135] "DRVEFDE2012.Percent.of.students.enrolled.in.some.but.not.all.distance.education.courses"                                                                
## [136] "DRVEFDE2012.Percent.of.students.not.enrolled.in.any.distance.education.courses"                                                                         
## [137] "DRVEFDE2012.Percent.of.undergraduate.students.enrolled.exclusively.in.distance.education.courses"                                                       
## [138] "DRVEFDE2012.Percent.of.undergraduate.students.enrolled.in.some.but.not.all.distance.education.courses"                                                  
## [139] "DRVEFDE2012.Percent.of.undergraduate.students.not.enrolled.in.any.distance.education.courses"                                                           
## [140] "DRVEFDE2012.Percent.of.graduate.students.enrolled.exclusively.in.distance.education.courses"                                                            
## [141] "DRVEFDE2012.Percent.of.graduate.students.enrolled.in.some.but.not.all.distance.education.courses"                                                       
## [142] "DRVEFDE2012.Percent.of.graduate.students.not.enrolled.in.any.distance.education.courses"                                                                
## [143] "DRVEF122012.12.month.unduplicated.headcount..total..2011.12"                                                                                            
## [144] "DRVEF122012.12.month.unduplicated.headcount..undergraduate..2011.12"                                                                                    
## [145] "DRVEF122012.12.month.full.time.equivalent.enrollment..2011.12"                                                                                          
## [146] "DRVC2012.Associate.s.degree"                                                                                                                            
## [147] "DRVC2012.Bachelor.s.degree"                                                                                                                             
## [148] "DRVC2012.Master.s.degree"                                                                                                                               
## [149] "DRVC2012.Doctor.s.degree...research.scholarship"                                                                                                        
## [150] "DRVC2012.Doctor.s.degree...professional.practice"                                                                                                       
## [151] "DRVC2012.Doctor.s.degree...other"                                                                                                                       
## [152] "DRVC2012.Certificates.of.less.than.1.year"                                                                                                              
## [153] "DRVC2012.Certificates.of.1.but.less.than.2.years"                                                                                                       
## [154] "DRVC2012.Certificates.of.2.but.less.than.4.years"                                                                                                       
## [155] "DRVC2012.Postbaccalaureate.certificates"                                                                                                                
## [156] "DRVC2012.Post.master.s.certificates"                                                                                                                    
## [157] "DRVC2012.Number.of.students.receiving.an.Associate.s.degree"                                                                                            
## [158] "DRVC2012.Number.of.students.receiving.a.Bachelor.s.degree"                                                                                              
## [159] "DRVC2012.Number.of.students.receiving.a.Master.s.degree"                                                                                                
## [160] "DRVC2012.Number.of.students.receiving.a.Doctor.s.degree"                                                                                                
## [161] "DRVC2012.Number.of.students.receiving.a.certificate.of.less.than.1.year"                                                                                
## [162] "DRVC2012.Number.of.students.receiving.a.certificate.of.1.but.less.than.4.years"                                                                         
## [163] "DRVC2012.Number.of.students.receiving.a.Postbaccalaureate.or.Post.master.s.certificate"                                                                 
## [164] "DRVGR2012.Graduation.rate..total.cohort"                                                                                                                
## [165] "DRVGR2012.Graduation.rate..men"                                                                                                                         
## [166] "DRVGR2012.Graduation.rate..women"                                                                                                                       
## [167] "DRVGR2012.Graduation.rate..American.Indian.or.Alaska.Native"                                                                                            
## [168] "DRVGR2012.Graduation.rate..Asian.Native.Hawaiian.Other.Pacific.Islander"                                                                                
## [169] "DRVGR2012.Graduation.rate..Asian"                                                                                                                       
## [170] "DRVGR2012.Graduation.rate..Native.Hawaiian.or.Other.Pacific.Islander"                                                                                   
## [171] "DRVGR2012.Graduation.rate..Black..non.Hispanic"                                                                                                         
## [172] "DRVGR2012.Graduation.rate..Hispanic"                                                                                                                    
## [173] "DRVGR2012.Graduation.rate..White..non.Hispanic"                                                                                                         
## [174] "DRVGR2012.Graduation.rate..two.or.more.races"                                                                                                           
## [175] "DRVGR2012.Graduation.rate..Race.ethnicity.unknown"                                                                                                      
## [176] "DRVGR2012.Graduation.rate..Nonresident.alien"                                                                                                           
## [177] "DRVGR2012.Transfer.out.rate..total.cohort"                                                                                                              
## [178] "GR200_12.Graduation.rate...degree.certificate.within.100..of.normal.time"                                                                               
## [179] "GR200_12.Graduation.rate...degree.certificate.within.150..of.normal.time"                                                                               
## [180] "GR200_12.Graduation.rate...degree.certificate.within.200..of.normal.time"                                                                               
## [181] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.4.years..total"                                                                                    
## [182] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.5.years..total"                                                                                    
## [183] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..total"                                                                                    
## [184] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..men"                                                                                      
## [185] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..women"                                                                                    
## [186] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..American.Indian.or.Alaska.Native"                                                         
## [187] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Asian.Native.Hawaiian.Pacific.Islander"                                                   
## [188] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Asian"                                                                                    
## [189] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Native.Hawaiian.or.Other.Pacific.Islander"                                                
## [190] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Black..non.Hispanic"                                                                      
## [191] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Hispanic"                                                                                 
## [192] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..White..non.Hispanic"                                                                      
## [193] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..two.or.more.races"                                                                        
## [194] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Race.ethnicity.unknown"                                                                   
## [195] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Nonresident.alien"                                                                        
## [196] "DRVGR2012.Transfer.out.rate...bachelor.s.cohort"                                                                                                        
## [197] "GR200_12.Graduation.rate...bachelor.s.degree.within.100..of.normal.time..4.years."                                                                      
## [198] "GR200_12.Graduation.rate...bachelor.s.degree.within.150..of.normal.time..6.years."                                                                      
## [199] "GR200_12.Graduation.rate...bachelor.s.degree.within.200..of.normal.time..8.years."                                                                      
## [200] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.any.financial.aid"                                                                     
## [201] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.federal..state..local.or.institutional.grant.aid"                                      
## [202] "SFA1112.Average.amount.of.federal..state..local.or.institutional.grant.aid.received"                                                                    
## [203] "SFA1112.Percent.of.full.time.first.time.undergraduates..receiving.federal.grant.aid"                                                                    
## [204] "SFA1112.Average.amount.of.federal.grant.aid.received.by.full.time.first.time.undergraduates"                                                            
## [205] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.Pell.grants"                                                                           
## [206] "SFA1112.Average.amount.of.Pell.grant.aid.received.by.full.time.first.time.undergraduates"                                                               
## [207] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.other.federal.grant.aid"                                                               
## [208] "SFA1112.Average.amount.of.other.federal.grant.aid.received.by.full.time.first.time.undergraduates"                                                      
## [209] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.state.local.grant.aid"                                                                 
## [210] "SFA1112.Average.amount.of.state.local.grant.aid.received.by.full.time.first.time.undergraduates"                                                        
## [211] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.institutional.grant.aid"                                                               
## [212] "SFA1112.Average.amount.of.institutional.grant.aid.received.by.full.time.first.time.undergraduates"                                                      
## [213] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.student.loan.aid"                                                                      
## [214] "SFA1112.Average.amount.of.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                             
## [215] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.federal.student.loans"                                                                 
## [216] "SFA1112.Average.amount.of.federal.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                     
## [217] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.other.loan.aid"                                                                        
## [218] "SFA1112.Average.amount.of.other.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                       
## [219] "DRVF2012.Core.revenues..total.dollars..GASB."                                                                                                           
## [220] "DRVF2012.Tuition.and.fees.as.a.percent.of.core.revenues..GASB."                                                                                         
## [221] "DRVF2012.State.appropriations.as.percent.of.core.revenues...GASB."                                                                                      
## [222] "DRVF2012.Local.appropriations.as.a.percent.of.core.revenues..GASB."                                                                                     
## [223] "DRVF2012.Government.grants.and.contracts.as.a.percent.of.core.revenues..GASB."                                                                          
## [224] "DRVF2012.Private.gifts..grants..and.contracts.as.a.percent.of.core.revenues..GASB."                                                                     
## [225] "DRVF2012.Investment.return.as.a.percent.of.core.revenues..GASB."                                                                                        
## [226] "DRVF2012.Other.revenues.as.a.percent.of.core.revenues..GASB."                                                                                           
## [227] "DRVF2012.Core.revenues..total.dollars..FASB."                                                                                                           
## [228] "DRVF2012.Tuition.and.fees.as.a.percent.of.core.revenues..FASB."                                                                                         
## [229] "DRVF2012.Government.grants.and.contracts.as.a.percent.of.core.revenues..FASB."                                                                          
## [230] "DRVF2012.Private.gifts..grants..contracts.contributions.from.affiliated.entities.as.a.percent.of.core.revenues..FASB."                                  
## [231] "DRVF2012.Investment.return.as.a.percent.of.core.revenues..FASB."                                                                                        
## [232] "DRVF2012.Other.revenues.as.a.percent.of.core.revenues..FASB."                                                                                           
## [233] "DRVF2012.Core.revenues..total.dollars..for.profit.institutions."                                                                                        
## [234] "DRVF2012.Tuition.and.fees.as.a.percent.of.core.revenues..for.profit.institutions."                                                                      
## [235] "DRVF2012.Govenment.appropriations..grants..and.contracts.as.a.percent.of.core.revenues..for.profit.institutions."                                       
## [236] "DRVF2012.Sales.and.services.of.educational.activities.as.a.percent.of.core.revenues..for.profit.institutions."                                          
## [237] "DRVF2012.Other.revenues.as.a.percent.of.core.revenues..for.profit.institutions."                                                                        
## [238] "DRVF2012.Revenues.from.tuition.and.fees.per.FTE..GASB."                                                                                                 
## [239] "DRVF2012.Revenues.from.state.appropriations.per.FTE..GASB."                                                                                             
## [240] "DRVF2012.Revenues.from.local.appropriations.per.FTE..GASB."                                                                                             
## [241] "DRVF2012.Revenues.from.government.grants.and.contracts.per.FTE..GASB."                                                                                  
## [242] "DRVF2012.Revenues.from.private.gifts..grants..and.contracts.per.FTE..GASB."                                                                             
## [243] "DRVF2012.Revenues.from.investment.return.per.FTE..GASB."                                                                                                
## [244] "DRVF2012.Other.core.revenues.per.FTE..GASB."                                                                                                            
## [245] "DRVF2012.Revenues.from.tuition.and.fees.per.FTE..FASB."                                                                                                 
## [246] "DRVF2012.Revenues.from.government.grants.and.contracts.per.FTE..FASB."                                                                                  
## [247] "DRVF2012.Revenues.from.private.gifts..grants..contracts.contributions.from.affiliated.entities.per.FTE..FASB."                                          
## [248] "DRVF2012.Revenues.from.investment.return.per.FTE..FASB."                                                                                                
## [249] "DRVF2012.Other.core.revenues.per.FTE..FASB."                                                                                                            
## [250] "DRVF2012.Revenues.from.tuition.and.fees.per.FTE..for.profit.institutions."                                                                              
## [251] "DRVF2012.Revenues.from.government.appropriations..grants.and.contracts.per.FTE..for.profit.institutions."                                               
## [252] "DRVF2012.Revenues.from.sales.and.services.of.educational.activities.per.FTE...for.profit.institutions."                                                 
## [253] "DRVF2012.Other.core.revenues.per.FTE..for.profit.institutions."                                                                                         
## [254] "DRVF2012.Core.expenses..total.dollars..GASB."                                                                                                           
## [255] "DRVF2012.Instruction.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                               
## [256] "DRVF2012.Research.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                                  
## [257] "DRVF2012.Public.service.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                            
## [258] "DRVF2012.Academic.support.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                          
## [259] "DRVF2012.Student.service.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                           
## [260] "DRVF2012.Institutional.support.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                     
## [261] "DRVF2012.Other.core.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                                
## [262] "DRVF2012.Core.expenses..total.dollars..FASB."                                                                                                           
## [263] "DRVF2012.Instruction.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                               
## [264] "DRVF2012.Research.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                                  
## [265] "DRVF2012.Public.service.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                            
## [266] "DRVF2012.Academic.support.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                          
## [267] "DRVF2012.Student.service.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                           
## [268] "DRVF2012.Institutional.support.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                     
## [269] "DRVF2012.Other.core.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                                
## [270] "DRVF2012.Core.expenses..total.dollars..for.profit.institutons."                                                                                         
## [271] "DRVF2012.Instruction.expenses.as.a.percent.of.total.core.expenses..for.profit.institutions."                                                            
## [272] "DRVF2012.Academic.and.institutional.support..and.student.service.expenses.as.a.percent.of.total.core.expenses..for.profit.institutions."                
## [273] "DRVF2012.Other.core.expenses.as.a.percent.of.total..core.expenses..for.profit.institutions."                                                            
## [274] "DRVF2012.Instruction.expenses.per.FTE...GASB."                                                                                                          
## [275] "DRVF2012.Research.expenses.per.FTE...GASB."                                                                                                             
## [276] "DRVF2012.Public.service.expenses.per.FTE..GASB."                                                                                                        
## [277] "DRVF2012.Academic.support.expenses.per.FTE..GASB."                                                                                                      
## [278] "DRVF2012.Student.service.expenses.per.FTE..GASB."                                                                                                       
## [279] "DRVF2012.Institutional.support.expenses.per.FTE..GASB."                                                                                                 
## [280] "DRVF2012.All.other.core.expenses.per.FTE..GASB."                                                                                                        
## [281] "DRVF2012.Instruction.expenses.per.FTE...FASB."                                                                                                          
## [282] "DRVF2012.Research.expenses.per.FTE..FASB."                                                                                                              
## [283] "DRVF2012.Public.service.expenses.per.FTE..FASB."                                                                                                        
## [284] "DRVF2012.Academic.support.expenses.per.FTE..FASB."                                                                                                      
## [285] "DRVF2012.Student.service.expenses.per.FTE..FASB."                                                                                                       
## [286] "DRVF2012.Institutional.support.expenses.per.FTE..FASB."                                                                                                 
## [287] "DRVF2012.All.other.core.expenses.per.FTE..FASB."                                                                                                        
## [288] "DRVF2012.Instruction.expenses.per.FTE..for.profit.institutions."                                                                                        
## [289] "DRVF2012.Academic.and.institutional.support..and.student.services..expense.per.FTE..for.profit.institutions."                                           
## [290] "DRVF2012.All.other.core.expenses.per.FTE..for.profit.institutions."                                                                                     
## [291] "DRVF2012.Salaries..wages..and.benefit.expenses.for.core.expenses.as.a.percent.of.total.core.expenses..GASB."                                            
## [292] "DRVF2012.Salaries..wages..and.benefit.expenses.for.instruction.as.a.percent.of.total.expenses.for.instruction..GASB."                                   
## [293] "DRVF2012.Salaries..wages..and.benefit.expenses.for.research.as.a.percent.of.total.expenses.for.research..GASB."                                         
## [294] "DRVF2012.Salaries..wages..and.benefit.expenses.for.public.service.as.a.percent.of.total.expenses.for.public.service..GASB."                             
## [295] "DRVF2012.Salaries..wages..and.benefit.expenses.for.academic.support.as.a.percent.of.total.expenses.for.academic.support..GASB."                         
## [296] "DRVF2012.Salaries..wages..and.benefit.expenses.for.student.services.as.a.percent.of.total.expenses.for.student.services..GASB."                         
## [297] "DRVF2012.Salaries..wages..and.benefit.expenses.for.institutional.support.as.a.percent.of.total.expenses.for.institutional.support..GASB."               
## [298] "DRVF2012.Salaries..wages..and.benefit.expenses.for.other.core.expense.functions..as.a.percent.of.total.expenses.for.other.core.expense.functions..GASB."
## [299] "DRVF2012.Total.salaries..wages..and.benefit.expenses.as.a.percent.of.total.expenses..GASB."                                                             
## [300] "DRVF2012.Total.salaries.and.wage.expenses.as.a.percent.of.total.expenses..GASB."                                                                        
## [301] "DRVF2012.Salaries..wages..and.benefit.expenses.for.core.expenses.as.a.percent.of.total.core.expenses..FASB."                                            
## [302] "DRVF2012.Salaries..wages..and.benefit.expenses.for.instruction.as.a.percent.of.total.expenses.for.instruction..FASB."                                   
## [303] "DRVF2012.Salaries..wages..and.benefit.expenses.for.research.as.a.percent.of.total.expenses.for.research..FASB."                                         
## [304] "DRVF2012.Salaries..wages..and.benefit.expenses.for.public.service.as.a.percent.of.total.expenses.for.public.service..FASB."                             
## [305] "DRVF2012.Salaries..wages..and.benefit.expenses.for.academic.support.as.a.percent.of.total.expenses.for.academic.support..FASB."                         
## [306] "DRVF2012.Salaries..wages..and.benefit.expenses.for.student.services.as.a.percent.of.total.expenses.for.student.services..FASB."                         
## [307] "DRVF2012.Salaries..wages..and.benefit.expenses.for.institutional.support.as.a.percent.of.total.expenses.for.institutional.support..FASB."               
## [308] "DRVF2012.Salaries..wages..and.benefit.expenses.for.other.core.expense.functions..as.a.percent.of.total.expenses.for.other.core.expense.functions..FASB."
## [309] "DRVF2012.Total.salaries..wages..and.benefit.expenses.as.a.percent.of.total.expenses..FASB."                                                             
## [310] "DRVF2012.Total.salaries.and.wage.expenses.as.a.percent.of.total.expenses..FASB."                                                                        
## [311] "DRVF2012.Endowment.assets..year.end..per.FTE.enrollment..GASB."                                                                                         
## [312] "DRVF2012.Endowment.assets..year.end..per.FTE.enrollment..FASB."                                                                                         
## [313] "DRVF2012.Equity.ratio..GASB."                                                                                                                           
## [314] "DRVF2012.Equity.ratio..FASB."                                                                                                                           
## [315] "DRVF2012.Equity.ratio..for.profit.institutions."                                                                                                        
## [316] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...all.ranks"                                                              
## [317] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.insructional.staff...professors"                                                              
## [318] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...associate.professors"                                                   
## [319] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...assistant.professors"                                                   
## [320] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...instructors"                                                            
## [321] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...lecturers"                                                              
## [322] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...No.academic.rank"                                                       
## [323] "DRVHR2012.Total.FTE.staff"                                                                                                                              
## [324] "DRVHR2012.Postsecondary.Teachers.FTE.staff"                                                                                                             
## [325] "DRVHR2012.Postsecondary.Teachers.Instructional.FTE"                                                                                                     
## [326] "DRVHR2012.Postsecondary.Teachers.Research.FTE"                                                                                                          
## [327] "DRVHR2012.Postsecondary.Teachers.Public.Service.FTE"                                                                                                    
## [328] "DRVHR2012.Librarians..Curators..and.Archivists.and.other.teaching.and.Instructional.support.occupations"                                                
## [329] "DRVHR2012.Librarians..Curators..and.Archivists.FTE"                                                                                                     
## [330] "DRVHR2012.Other.teaching.and.Instructional.Support.FTE"                                                                                                 
## [331] "DRVHR2012.Management.FTE"                                                                                                                               
## [332] "DRVHR2012.Business.and.Financial.Operations.FTE"                                                                                                        
## [333] "DRVHR2012.Computer..Engineering..and.Science.FTE"                                                                                                       
## [334] "DRVHR2012.Community.Service..Legal..Arts..and.Media.FTE"                                                                                                
## [335] "DRVHR2012.Healthcare.FTE"                                                                                                                               
## [336] "DRVHR2012.Service..sales..office.admin.support..natural.resources..construction..maintenance..production..transportation...materials.moving.FTE"        
## [337] "DRVHR2012.Service.FTE"                                                                                                                                  
## [338] "DRVHR2012.Sales.and.Related.FTE"                                                                                                                        
## [339] "DRVHR2012.Office.and.Administrative.Support.FTE"                                                                                                        
## [340] "DRVHR2012.Natural.Resources..Construction..and.Maintenance.FTE"                                                                                         
## [341] "DRVHR2012.Production..Transportation..and.Material.Moving.FTE"                                                                                          
## [342] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2011.12"                                                                         
## [343] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2010.11"                                                                         
## [344] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2009.10"                                                                         
## [345] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid.2011.12"                                                  
## [346] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                            
## [347] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                            
## [348] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                           
## [349] "SFA1112.Average.net.price..income.over.110.000...students.receiving.Title.IV.Federal.financial.aid..2011.12"                                            
## [350] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                                 
## [351] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                                 
## [352] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                            
## [353] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                            
## [354] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                            
## [355] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                            
## [356] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                           
## [357] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                           
## [358] "SFA1112.Average.net.price..income.over.110.000...students.receiving.Title.IV.Federal.financial.aid..2009.10"                                            
## [359] "SFA1112.Average.net.price..income.over.110.000...students.receiving.Title.IV.Federal.financial.aid..2010.11"                                            
## [360] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2011.12.1"                                                                       
## [361] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2010.11.1"                                                                       
## [362] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2009.10.1"                                                                       
## [363] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                                 
## [364] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2011.12.1"                                          
## [365] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2011.12.1"                                          
## [366] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid.2011.12"                                            
## [367] "SFA1112.Average.net.price..income.over.110.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                             
## [368] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                               
## [369] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                               
## [370] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                          
## [371] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                          
## [372] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                          
## [373] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                          
## [374] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                         
## [375] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                         
## [376] "SFA1112.Average.net.price..income.over.110.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                             
## [377] "SFA1112.Average.net.price..income.over.110.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"
```

```r
str(df1)
```

```
## 'data.frame':	380 obs. of  377 variables:
##  $ unitid                                                                                                                                                 : int  125231 142887 143048 143084 143118 143288 143358 144005 144050 144281 ...
##  $ institution.name                                                                                                                                       : Factor w/ 378 levels "Adrian College",..: 357 8 265 20 21 32 35 56 299 68 ...
##  $ year                                                                                                                                                   : int  2012 2012 2012 2012 2012 2012 2012 2012 2012 2012 ...
##  $ DRVIC2012.Percent.admitted...total                                                                                                                     : int  NA 92 78 69 75 61 63 38 13 NA ...
##  $ DRVIC2012.Percent.admitted...men                                                                                                                       : int  NA 99 90 64 77 61 64 32 14 NA ...
##  $ DRVIC2012.Percent.admitted...women                                                                                                                     : int  NA 88 75 73 73 61 63 41 13 NA ...
##  $ DRVIC2012.Admissions.yield...total                                                                                                                     : int  NA 47 24 23 32 47 21 22 46 NA ...
##  $ DRVIC2012.Admissions.yield...men                                                                                                                       : int  NA 46 25 24 32 49 24 25 48 NA ...
##  $ DRVIC2012.Admissions.yield...women                                                                                                                     : int  NA 48 24 22 32 45 19 20 43 NA ...
##  $ DRVIC2012.Admissions.yield...full.time                                                                                                                 : int  NA 33 24 23 32 46 21 18 46 NA ...
##  $ DRVIC2012.Admissions.yield...full.time.men                                                                                                             : int  NA 32 25 24 32 48 24 19 48 NA ...
##  $ DRVIC2012.Admissions.yield...full.time.women                                                                                                           : int  NA 35 24 22 32 44 19 17 43 NA ...
##  $ DRVIC2012.Admissions.yield...part.time                                                                                                                 : int  NA 14 0 0 0 1 0 4 0 NA ...
##  $ DRVIC2012.Admissions.yield...part.time.men                                                                                                             : int  NA 14 0 0 0 1 0 5 0 NA ...
##  $ DRVIC2012.Admissions.yield...part.time.women                                                                                                           : int  NA 13 0 0 0 1 0 3 0 NA ...
##  $ DRVIC2012.Tuition.and.fees..2009.10                                                                                                                    : int  12140 24250 34770 31326 18200 14286 24224 8006 40286 18960 ...
##  $ DRVIC2012.Tuition.and.fees..2010.11                                                                                                                    : int  9480 25570 36150 32235 18700 14996 25424 8752 42041 19610 ...
##  $ DRVIC2012.Tuition.and.fees..2011.12                                                                                                                    : int  10610 26570 37560 33363 19450 16296 26704 9062 43780 20644 ...
##  $ DRVIC2012.Tuition.and.fees..2012.13                                                                                                                    : int  11010 27770 39020 34614 20100 17502 28284 8558 45609 21730 ...
##  $ DRVIC2012.Total.price.for.in.district.students.living.on.campus..2012.13                                                                               : int  NA NA 56560 45598 32356 24584 40330 22480 62425 38890 ...
##  $ DRVIC2012.Total.price.for.in.state.students.living.on.campus.2012.13                                                                                   : int  NA NA 56560 45598 32356 24584 40330 22480 62425 38890 ...
##  $ DRVIC2012.Total.price.for.out.of.state.students.living.on.campus.2012.13                                                                               : int  NA NA 56560 45598 32356 24584 40330 28576 62425 38890 ...
##  $ DRVIC2012.Total.price.for.in.district.students.living.off.campus..not.with.family...2012.13                                                            : int  31410 38124 54050 41814 29498 20552 40330 22480 NA 38890 ...
##  $ DRVIC2012.Total.price.for.in.state.students.living.off.campus..not.with.family...2012.13                                                               : int  31410 38124 54050 41814 29498 20552 40330 22480 NA 38890 ...
##  $ DRVIC2012.Total.price.for.out.of.state.students.living.off.campus..not.with.family...2012.13                                                           : int  31410 38124 54050 41814 29498 20552 40330 28576 NA 38890 ...
##  $ DRVIC2012.Total.price.for.in.district.students.living.off.campus..with.family...2012.13                                                                : int  17910 31770 42750 36814 29498 19052 33780 14258 NA 26970 ...
##  $ DRVIC2012.Total.price.for.in.state.students.living.off.campus..with.family...2012.13                                                                   : int  17910 31770 42750 36814 29498 19052 33780 14258 NA 26970 ...
##  $ DRVIC2012.Total.price.for.out.of.state.students.living.off.campus..with.family...2012.13                                                               : int  17910 31770 42750 36814 29498 19052 33780 20354 NA 26970 ...
##  $ HD2012.Institution.size.category                                                                                                                       : Factor w/ 5 levels "1,000 - 4,999",..: 3 5 1 1 1 5 4 4 2 2 ...
##  $ HD2012.State.abbreviation                                                                                                                              : Factor w/ 7 levels "Illinois","Indiana",..: 5 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.FIPS.state.code                                                                                                                                 : Factor w/ 7 levels "Illinois","Indiana",..: 5 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Geographic.region                                                                                                                               : Factor w/ 2 levels "Great Lakes IL IN MI OH WI",..: 2 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Sector.of.institution                                                                                                                           : Factor w/ 3 levels "Private for-profit, 4-year or above",..: 1 1 2 2 2 2 2 3 2 2 ...
##  $ HD2012.Level.of.institution                                                                                                                            : Factor w/ 1 level "Four or more years": 1 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Control.of.institution                                                                                                                          : Factor w/ 3 levels "Private for-profit",..: 1 1 2 2 2 2 2 3 2 2 ...
##  $ HD2012.Degree.granting.status                                                                                                                          : Factor w/ 1 level "Degree-granting": 1 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Historically.Black.College.or.University                                                                                                        : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Tribal.college                                                                                                                                  : Factor w/ 1 level "No": 1 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Degree.of.urbanization..Urban.centric.locale.                                                                                                   : Factor w/ 12 levels "City: Large",..: 1 1 1 3 7 10 2 1 1 1 ...
##  $ HD2012.Postsecondary.and.Title.IV.institution.indicator                                                                                                : Factor w/ 2 levels "Non-Title IV postsecondary institution",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Institutional.category                                                                                                                          : Factor w/ 1 level "Degree-granting, primarily baccalaureate or above": 1 1 1 1 1 1 1 1 1 1 ...
##  $ HD2012.Carnegie.Classification.2010..Basic                                                                                                             : Factor w/ 17 levels "Associate's--Private For-profit 4-year Primarily Associate's",..: 6 14 14 3 7 4 7 7 13 8 ...
##  $ HD2012.Carnegie.Classification.2010..Undergraduate.Instructional.Program                                                                               : Factor w/ 19 levels "Arts & sciences focus, high graduate coexistence",..: 14 12 12 5 19 9 19 10 1 19 ...
##  $ HD2012.Carnegie.Classification.2010..Graduate.Instructional.Program                                                                                    : Factor w/ 20 levels "Comprehensive doctoral (no medical/veterinary)",..: 3 6 6 4 15 4 13 15 2 13 ...
##  $ HD2012.Carnegie.Classification.2010..Undergraduate.Profile                                                                                             : Factor w/ 11 levels "Full-time four-year, inclusive",..: 6 11 11 3 4 5 2 7 3 1 ...
##  $ HD2012.Carnegie.Classification.2010..Enrollment.Profile                                                                                                : Factor w/ 6 levels "Exclusively undergraduate four-year",..: 3 1 2 1 4 1 6 2 3 6 ...
##  $ HD2012.Carnegie.Classification.2010..Size.and.Setting                                                                                                  : Factor w/ 14 levels "Large four-year, highly residential",..: 2 8 8 9 6 12 4 5 1 2 ...
##  $ HD2012.Land.Grant.Institution                                                                                                                          : Factor w/ 2 levels "Land Grant Institution",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Carnegie.Classification.2000                                                                                                                    : Factor w/ 16 levels "{Item not available}",..: 7 12 12 4 8 4 8 8 6 8 ...
##  $ HD2012.Data.Feedback.Report.comparison.group.category.created.by.NCES                                                                                  : Factor w/ 78 levels "Baccalaureate Colleges--Arts & Sciences or Diverse Fields, private for-profit /1 of 2",..: 58 67 68 4 28 17 27 36 63 39 ...
##  $ HD2012.Data.Feedback.Report...Institution.submitted.a..custom.comparison.group                                                                         : Factor w/ 2 levels "No, institution did not submit a custom comparison group",..: 2 1 2 2 2 1 2 1 2 1 ...
##  $ HD2012.Institution.size.category.1                                                                                                                     : Factor w/ 5 levels "1,000 - 4,999",..: 3 5 1 1 1 5 4 4 2 2 ...
##  $ DRVEF2012.Total..enrollment                                                                                                                            : int  50209 432 3310 2551 4681 546 5458 6107 15245 10783 ...
##  $ DRVEF2012.Full.time.enrollment                                                                                                                         : int  30597 316 3034 2532 3048 531 4867 3796 12720 9590 ...
##  $ DRVEF2012.Part.time.enrollment                                                                                                                         : int  19612 116 276 19 1633 15 591 2311 2525 1193 ...
##  $ DRVEF2012.Full.time.equivalent.fall.enrollment                                                                                                         : int  38174 362 3142 2539 3676 537 5095 4699 13685 10058 ...
##  $ DRVEF2012.Undergraduate.enrollment                                                                                                                     : int  8696 432 2629 2551 2994 546 4879 4618 5618 10310 ...
##  $ DRVEF2012.First.time.degree.certificate.seeking.undergraduate.enrollment                                                                               : int  327 114 563 656 523 138 1016 323 1527 2091 ...
##  $ DRVEF2012.Transfer.in.degree.certificate.seeking.undergraduate.enrollment                                                                              : int  2318 9 239 52 466 60 286 556 16 903 ...
##  $ DRVEF2012.Continuing.degree.certificate.seeking.undergraduate.enrollment                                                                               : int  5913 309 1753 1823 1992 343 3571 3714 4069 7214 ...
##  $ DRVEF2012.Nondegree.certificate.seeking.undergraduate.enrollment                                                                                       : int  138 0 74 20 13 5 6 25 6 102 ...
##  $ DRVEF2012.Graduate.enrollment                                                                                                                          : int  41513 0 681 0 1687 0 579 1489 9627 473 ...
##  $ DRVEF2012.Full.time.undergraduate.enrollment                                                                                                           : int  887 316 2387 2532 2608 531 4632 3012 5559 9224 ...
##  $ DRVEF2012.Full.time.first.time.degree.certificate.seeking.undergraduate.enrollment                                                                     : int  1 81 561 656 523 135 1015 263 1527 2024 ...
##  $ DRVEF2012.Full.time.transfer.in.degree.certificate.seeking.undergraduate.enrollment                                                                    : int  158 8 222 52 383 60 262 415 15 820 ...
##  $ DRVEF2012.Full.time.continuing.degree.certificate.seeking.undergraduate.enrollment                                                                     : int  728 227 1603 1809 1702 334 3355 2329 4012 6354 ...
##  $ DRVEF2012.Full.time.nondegree.certificate.seeking.undergraduate.enrollment                                                                             : int  0 0 1 15 0 2 0 5 5 26 ...
##  $ DRVEF2012.Full.time.graduate.enrollment                                                                                                                : int  29710 0 647 0 440 0 235 784 7161 366 ...
##  $ DRVEF2012.Part.time.undergraduate.enrollment                                                                                                           : int  7809 116 242 19 386 15 247 1606 59 1086 ...
##  $ DRVEF2012.Part.time.first.time.degree.certificate.seeking.undergraduate.enrollment                                                                     : int  326 33 2 0 0 3 1 60 0 67 ...
##  $ DRVEF2012.Part.time.transfer.in.degree.certificate.seeking.undergraduate.enrollment                                                                    : int  2160 1 17 0 83 0 24 141 1 83 ...
##  $ DRVEF2012.Part.time.continuing.degree.certificate.seeking.undergraduate.enrollment                                                                     : int  5185 82 150 14 290 9 216 1385 57 860 ...
##  $ DRVEF2012.Part.time.nondegree.certificate.seeking.undergraduate.enrollment                                                                             : int  138 0 73 5 13 3 6 20 1 76 ...
##  $ DRVEF2012.Part.time.graduate.enrollment                                                                                                                : int  11803 0 34 0 1247 0 344 705 2466 107 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.American.Indian.or.Alaska.Native                                                                        : int  1 0 1 0 0 1 0 0 0 0 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Asian                                                                                                   : int  2 3 10 2 2 1 3 3 13 3 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Black.or.African.American                                                                               : int  37 13 4 4 8 8 7 78 4 17 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Hispanic.Latino                                                                                         : int  5 25 5 7 14 1 5 6 6 13 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander                                                               : int  0 1 0 0 0 1 0 0 0 0 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.White                                                                                                   : int  41 55 53 80 70 85 79 6 45 57 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.two.or.more.races                                                                                       : int  2 3 3 2 2 1 1 0 3 3 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Race.ethnicity.unknown                                                                                  : int  12 0 2 3 5 2 1 6 10 5 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Nonresident.Alien                                                                                       : int  1 0 22 2 0 0 3 0 20 2 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander                                                                  : int  2 4 11 2 2 1 3 3 13 3 ...
##  $ DRVEF2012.Percent.of.total.enrollment.that.are.women                                                                                                   : int  77 56 70 57 68 58 53 71 42 54 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.American.Indian.or.Alaska.Native                                                                : int  0 0 1 0 0 1 0 0 0 0 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Asian                                                                                           : int  1 3 12 2 2 1 4 1 18 3 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Black.or.African.American                                                                       : int  36 13 4 4 8 8 7 83 5 17 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Hispanic.Latino                                                                                 : int  6 25 6 7 17 1 6 7 8 13 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander                                                       : int  0 1 0 0 0 1 0 0 0 0 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.White                                                                                           : int  41 55 51 80 67 85 80 3 46 57 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.two.or.more.races                                                                               : int  2 3 3 2 2 1 1 0 3 3 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Race.ethnicity.unknown                                                                          : int  13 0 2 3 3 2 1 6 10 5 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Nonresident.Alien                                                                               : int  1 0 21 2 0 0 1 0 9 2 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander                                                          : int  1 4 12 2 2 1 4 1 18 3 ...
##  $ DRVEF2012.Percent.of.undergraduate.enrollment.that.are.women                                                                                           : int  75 56 70 57 64 58 53 72 47 53 ...
##  $ DRVEF2012.Percent.of.graduate.enrollment.that.are.American.Indian.or.Alaska.Native                                                                     : int  1 NA 0 NA 1 NA 0 0 0 0 ...
##  $ DRVEF2012.Percent.of.graduate.enrollment.that.are.Asian                                                                                                : int  2 NA 5 NA 1 NA 2 10 10 1 ...
##  $ DRVEF2012.Percent.of.graduate.enrollment.that.are.Black.or.African.American                                                                            : int  37 NA 4 NA 7 NA 4 63 4 12 ...
##   [list output truncated]
```




Category 2: Institutional characteristics
---------------------------------------------


```r
df2 <- read.csv("2012/raw/02_Institutional_characteristics.csv")
dim(df2)
```

```
## [1] 6280  456
```

```r
names(df2)
```

```
##   [1] "unitid"                                                                                                                             
##   [2] "institution.name"                                                                                                                   
##   [3] "year"                                                                                                                               
##   [4] "institution.name.1"                                                                                                                 
##   [5] "HD2012.Street.address.or.post.office.box"                                                                                           
##   [6] "HD2012.City.location.of.institution"                                                                                                
##   [7] "HD2012.State.abbreviation"                                                                                                          
##   [8] "HD2012.ZIP.code"                                                                                                                    
##   [9] "HD2012.FIPS.state.code"                                                                                                             
##  [10] "HD2012.Geographic.region"                                                                                                           
##  [11] "HD2012.Name.of.chief.administrator"                                                                                                 
##  [12] "HD2012.Title.of.chief.administrator"                                                                                                
##  [13] "HD2012.General.information.telephone.number"                                                                                        
##  [14] "HD2012.Fax.number"                                                                                                                  
##  [15] "HD2012.Institution.s.internet.website.address"                                                                                      
##  [16] "HD2012.Financial.aid.office.web.address"                                                                                            
##  [17] "HD2012.Admissions.office.web.address"                                                                                               
##  [18] "HD2012.Online.application.web.address"                                                                                              
##  [19] "HD2012.Net.price.calculator.web.address"                                                                                            
##  [20] "HD2012.Office.of.Postsecondary.Education..OPE..ID.Number"                                                                           
##  [21] "HD2012.OPE.Title.IV.eligibility.indicator.code"                                                                                     
##  [22] "HD2012.Employer.Identification.Number"                                                                                              
##  [23] "HD2012.System..Governing.Board.or.Corporate.Structure"                                                                              
##  [24] "HD2012.Name.of.system..governing.board.or.corporate.entity."                                                                        
##  [25] "HD2012.Sector.of.institution"                                                                                                       
##  [26] "HD2012.Level.of.institution"                                                                                                        
##  [27] "HD2012.Control.of.institution"                                                                                                      
##  [28] "HD2012.Highest.level.of.offering"                                                                                                   
##  [29] "HD2012.Undergraduate.offering"                                                                                                      
##  [30] "HD2012.Graduate.offering"                                                                                                           
##  [31] "HD2012.Highest.degree.offered"                                                                                                      
##  [32] "HD2012.Degree.granting.status"                                                                                                      
##  [33] "HD2012.Historically.Black.College.or.University"                                                                                    
##  [34] "HD2012.Institution.has.hospital"                                                                                                    
##  [35] "HD2012.Institution.grants.a.medical.degree"                                                                                         
##  [36] "HD2012.Tribal.college"                                                                                                              
##  [37] "HD2012.Degree.of.urbanization..Urban.centric.locale."                                                                               
##  [38] "HD2012.Fips.County.code"                                                                                                            
##  [39] "HD2012.County.name"                                                                                                                 
##  [40] "HD2012.Congressional.district.code"                                                                                                 
##  [41] "HD2012.Core.Based.Statistical.Area..CBSA."                                                                                          
##  [42] "HD2012.CBSA.Type.Metropolitan.or.Micropolitan"                                                                                      
##  [43] "HD2012.Combined.Statistical.Area..CSA."                                                                                             
##  [44] "HD2012.New.England.City.and.Town.Area..NECTA."                                                                                      
##  [45] "HD2012.Longitude.location.of.institution"                                                                                           
##  [46] "HD2012.Latitude.location.of.institution"                                                                                            
##  [47] "HD2012.Institution.open.to.the.general.public"                                                                                      
##  [48] "HD2012.Status.of.institution"                                                                                                       
##  [49] "HD2012.UNITID.for.merged.schools"                                                                                                   
##  [50] "HD2012.Year.institution.was.deleted.from.IPEDS"                                                                                     
##  [51] "HD2012.Date.institution.closed"                                                                                                     
##  [52] "HD2012.Institution.is.active.in.current.year"                                                                                       
##  [53] "HD2012.Primarily.postsecondary.indicator"                                                                                           
##  [54] "HD2012.Postsecondary.institution.indicator"                                                                                         
##  [55] "HD2012.Postsecondary.and.Title.IV.institution.indicator"                                                                            
##  [56] "HD2012.Reporting.method.for.student.charges..graduation.rates..retention.rates.and.student.financial.aid"                           
##  [57] "HD2012.Institutional.category"                                                                                                      
##  [58] "HD2012.Carnegie.Classification.2010..Basic"                                                                                         
##  [59] "HD2012.Carnegie.Classification.2010..Undergraduate.Instructional.Program"                                                           
##  [60] "HD2012.Carnegie.Classification.2010..Graduate.Instructional.Program"                                                                
##  [61] "HD2012.Carnegie.Classification.2010..Undergraduate.Profile"                                                                         
##  [62] "HD2012.Carnegie.Classification.2010..Enrollment.Profile"                                                                            
##  [63] "HD2012.Carnegie.Classification.2010..Size.and.Setting"                                                                              
##  [64] "HD2012.Land.Grant.Institution"                                                                                                      
##  [65] "HD2012.Carnegie.Classification.2000"                                                                                                
##  [66] "HD2012.Data.Feedback.Report.comparison.group.category.created.by.NCES"                                                              
##  [67] "HD2012.Data.Feedback.Report...Institution.submitted.a..custom.comparison.group"                                                     
##  [68] "FLAGS2012.Status.of.IC.component.when.institution.was.migrated"                                                                     
##  [69] "FLAGS2012.Response.status....Institutional.characteristics.component"                                                               
##  [70] "FLAGS2012.Type.of.imputation.method.Institutional.Characteristics"                                                                  
##  [71] "FLAGS2012.Natural.Disaster.identification"                                                                                          
##  [72] "HD2012.Institution.name.alias"                                                                                                      
##  [73] "IC2012.Occupational"                                                                                                                
##  [74] "IC2012.Academic"                                                                                                                    
##  [75] "IC2012.Continuing.professional"                                                                                                     
##  [76] "IC2012.Recreational.or.avocational"                                                                                                 
##  [77] "IC2012.Adult.basic.remedial.or.high.school.equivalent"                                                                              
##  [78] "IC2012.Secondary..high.school."                                                                                                     
##  [79] "IC2012.Institutional.control.or.affiliation"                                                                                        
##  [80] "IC2012.Primary.public.control"                                                                                                      
##  [81] "IC2012.Secondary.public.control"                                                                                                    
##  [82] "IC2012.Religious.affiliation"                                                                                                       
##  [83] "IC2012.Less.than.one.year.certificate"                                                                                              
##  [84] "IC2012.One.but.less.than.two.years.certificate"                                                                                     
##  [85] "IC2012.Associate.s.degree"                                                                                                          
##  [86] "IC2012.Two.but.less.than.4.years.certificate"                                                                                       
##  [87] "IC2012.Bachelor.s.degree"                                                                                                           
##  [88] "IC2012.Postbaccalaureate.certificate"                                                                                               
##  [89] "IC2012.Master.s.degree"                                                                                                             
##  [90] "IC2012.Post.master.s.certificate"                                                                                                   
##  [91] "IC2012.Doctor.s.degree...research.scholarship"                                                                                      
##  [92] "IC2012.Doctor.s.degree...professional.practice"                                                                                     
##  [93] "IC2012.Doctor.s.degree...other"                                                                                                     
##  [94] "IC2012.Other.degree"                                                                                                                
##  [95] "IC2012.Open.admission.policy"                                                                                                       
##  [96] "IC2012.Secondary.school.GPA"                                                                                                        
##  [97] "IC2012.Secondary.school.rank"                                                                                                       
##  [98] "IC2012.Secondary.school.record"                                                                                                     
##  [99] "IC2012.Completion.of.college.preparatory.program"                                                                                   
## [100] "IC2012.Recommendations"                                                                                                             
## [101] "IC2012.Formal.demonstration.of.competencies"                                                                                        
## [102] "IC2012.Admission.test.scores"                                                                                                       
## [103] "IC2012.Other.Test..Wonderlic..WISC.III..etc.."                                                                                      
## [104] "IC2012.TOEFL..Test.of.English.as.a.Foreign.Language"                                                                                
## [105] "IC2012.Fall.reporting.period.for.applicant.and.admissions"                                                                          
## [106] "IC2012.Applicants.total"                                                                                                            
## [107] "IC2012.Applicants.men"                                                                                                              
## [108] "IC2012.Applicants.women"                                                                                                            
## [109] "IC2012.Admissions.total"                                                                                                            
## [110] "IC2012.Admissions.men"                                                                                                              
## [111] "IC2012.Admissions.women"                                                                                                            
## [112] "IC2012.Enrolled.total"                                                                                                              
## [113] "IC2012.Enrolled..men"                                                                                                               
## [114] "IC2012.Enrolled..women"                                                                                                             
## [115] "IC2012.Enrolled.full.time.total"                                                                                                    
## [116] "IC2012.Enrolled.full.time.men"                                                                                                      
## [117] "IC2012.Enrolled.full.time.women"                                                                                                    
## [118] "IC2012.Enrolled.part.time.total"                                                                                                    
## [119] "IC2012.Enrolled.part.time.men"                                                                                                      
## [120] "IC2012.Enrolled.part.time.women"                                                                                                    
## [121] "DRVIC2012.Percent.admitted...total"                                                                                                 
## [122] "DRVIC2012.Percent.admitted...men"                                                                                                   
## [123] "DRVIC2012.Percent.admitted...women"                                                                                                 
## [124] "DRVIC2012.Admissions.yield...total"                                                                                                 
## [125] "DRVIC2012.Admissions.yield...men"                                                                                                   
## [126] "DRVIC2012.Admissions.yield...women"                                                                                                 
## [127] "DRVIC2012.Admissions.yield...full.time"                                                                                             
## [128] "DRVIC2012.Admissions.yield...full.time.men"                                                                                         
## [129] "DRVIC2012.Admissions.yield...full.time.women"                                                                                       
## [130] "DRVIC2012.Admissions.yield...part.time"                                                                                             
## [131] "DRVIC2012.Admissions.yield...part.time.men"                                                                                         
## [132] "DRVIC2012.Admissions.yield...part.time.women"                                                                                       
## [133] "IC2012.Fall.reporting.period.for.SAT.ACT.test.scores"                                                                               
## [134] "IC2012.Number.of.first.time.degree.certificate.seeking.students.submitting.SAT.scores"                                              
## [135] "IC2012.Percent.of.first.time.degree.certificate.seeking.students.submitting.SAT.scores"                                             
## [136] "IC2012.Number.of.first.time.degree.certificate.seeking.students.submitting.ACT.scores"                                              
## [137] "IC2012.Percent.of.first.time.degree.certificate.seeking.students.submitting.ACT.scores"                                             
## [138] "IC2012.SAT.Critical.Reading.25th.percentile.score"                                                                                  
## [139] "IC2012.SAT.Critical.Reading.75th.percentile.score"                                                                                  
## [140] "IC2012.SAT.Math.25th.percentile.score"                                                                                              
## [141] "IC2012.SAT.Math.75th.percentile.score"                                                                                              
## [142] "IC2012.SAT.Writing.25th.percentile.score"                                                                                           
## [143] "IC2012.SAT.Writing.75th.percentile.score"                                                                                           
## [144] "IC2012.ACT.Composite.25th.percentile.score"                                                                                         
## [145] "IC2012.ACT.Composite.75th.percentile.score"                                                                                         
## [146] "IC2012.ACT.English.25th.percentile.score"                                                                                           
## [147] "IC2012.ACT.English.75th.percentile.score"                                                                                           
## [148] "IC2012.ACT.Math.25th.percentile.score"                                                                                              
## [149] "IC2012.ACT.Math.75th.percentile.score"                                                                                              
## [150] "IC2012.ACT.Writing.25th.percentile.score"                                                                                           
## [151] "IC2012.ACT.Writing.75th.percentile.score"                                                                                           
## [152] "IC2012.Dual.credit"                                                                                                                 
## [153] "IC2012.Credit.for.life.experiences"                                                                                                 
## [154] "IC2012.Advanced.placement..AP..credits"                                                                                             
## [155] "IC2012.Institution.does.not.accept.dual..credit.for.life..or.AP.credits"                                                            
## [156] "IC2012.All.programs.offered.completely.via.distance.education"                                                                      
## [157] "IC2012.Undergraduate.programs.or.courses.are.offered.via.distance.education"                                                        
## [158] "IC2012.Graduate.programs.or.courses.are.offered.via.distance.education"                                                             
## [159] "IC2012.Does.not.offer.distance.education.opportunities"                                                                             
## [160] "IC2012.ROTC"                                                                                                                        
## [161] "IC2012.ROTC...Army"                                                                                                                 
## [162] "IC2012.ROTC...Navy"                                                                                                                 
## [163] "IC2012.ROTC...Air.Force"                                                                                                            
## [164] "IC2012.Study.abroad"                                                                                                                
## [165] "IC2012.Weekend.evening..college"                                                                                                    
## [166] "IC2012.Teacher.certification..below.the.postsecondary.level."                                                                       
## [167] "IC2012.Teacher.certification..Students.can.complete.their.preparation.in.certain.areas.of.specialization"                           
## [168] "IC2012.Teacher.certification..Students.must.complete.their.preparation.at.another.institution.for.certain.areas.of.specialization"  
## [169] "IC2012.Teacher.certification..Approved.by.the.state.for.initial.certifcation.or.licensure.of.teachers."                             
## [170] "IC2012.None.of.the.above.special.learning.opportunities.are.offered"                                                                
## [171] "IC2012.Years.of.college.level.work.required"                                                                                        
## [172] "IC2012.Remedial.services"                                                                                                           
## [173] "IC2012.Academic.career.counseling.service"                                                                                          
## [174] "IC2012.Employment.services.for.students"                                                                                            
## [175] "IC2012.Placement.services.for.completers"                                                                                           
## [176] "IC2012.On.campus.day.care.for.students..children"                                                                                   
## [177] "IC2012.None.of.the.above.selected.services.are.offered"                                                                             
## [178] "IC2012.Library.facilities.at.institution"                                                                                           
## [179] "IC2012.Calendar.system"                                                                                                             
## [180] "IC2012.Any.alternative.tuition.plans.offered.by.institution"                                                                        
## [181] "IC2012.Tuition.guaranteed.plan"                                                                                                     
## [182] "IC2012.Prepaid.tuition.plan"                                                                                                        
## [183] "IC2012.Tuition.payment.plan"                                                                                                        
## [184] "IC2012.Other.alternative.tuition.plan"                                                                                              
## [185] "IC2012.Undergraduate.application.fee"                                                                                               
## [186] "IC2012.Graduate.application.fee"                                                                                                    
## [187] "IC2012.Full.time.undergraduate.students.are.enrolled"                                                                               
## [188] "IC2012.Full.time.first.time.degree.certificate.seeking.undergraduate.students.enrolled"                                             
## [189] "IC2012.Full.time.graduate..not.including.doctor.s.professional.practice..students.are.enrolled"                                     
## [190] "IC2012.Part.time.undergraduate.students.are.enrolled"                                                                               
## [191] "IC2012.Part.time.first.time.degree.certificate.seeking.undergraduate.students.enrolled"                                             
## [192] "IC2012.Part.time.graduate..not.including.doctor.s.professional.practice..students.are.enrolled"                                     
## [193] "IC2012.Doctor.s.professional.practice.students.are.enrolled"                                                                        
## [194] "IC2012.Doctor.s.professional.practice.students.are.enrolled.in.programs.formerly.designated.as.first.professional"                  
## [195] "IC2012.Tuition.charge.varies.for.in.district..in.state..out.of.state.students"                                                      
## [196] "IC2012.Full.time..first.time.degree.certificate.seeking.students.required.to.live.on.campus"                                        
## [197] "IC2012.Institution.provide.on.campus.housing"                                                                                       
## [198] "IC2012.Total.dormitory.capacity"                                                                                                    
## [199] "IC2012.Institution.provides.board.or.meal.plan"                                                                                     
## [200] "IC2012.Number.of.meals.per.week.in.board.charge"                                                                                    
## [201] "IC2012.Typical.room.charge.for.academic.year"                                                                                       
## [202] "IC2012.Typical.board.charge.for.academic.year"                                                                                      
## [203] "IC2012.Combined.charge.for.room.and.board"                                                                                          
## [204] "IC2012_PY.Number.of.programs.offered"                                                                                               
## [205] "IC2012_PY.CIP.code.of.largest.program"                                                                                              
## [206] "IC2012_PY.Total.length.of.largest.program"                                                                                          
## [207] "IC2012_PY.Largest.program.measured.in.credit.or.contact.hours"                                                                      
## [208] "IC2012_PY.Average.number.of.months.to.complete.largest.program"                                                                     
## [209] "IC2012_PY.Total.length.of.program.in.weeks..as.completed.by.a.student.attending.full.time"                                          
## [210] "IC2012_PY.Total.length.of.academic.year..as.used.to.calculate.your.Pell.budget..in.contact.or.credit.hours"                         
## [211] "IC2012_PY.Total.length.of.academic.year..as.used.to.calculate.your.Pell.budget..in.weeks"                                           
## [212] "IC2012_PY.Published.tuition.and.fees.2009.10"                                                                                       
## [213] "IC2012_PY.Published.tuition.and.fees.2010.11"                                                                                       
## [214] "IC2012_PY.Published.tuition.and.fees.2011.12"                                                                                       
## [215] "IC2012_PY.Published.tuition.and.fees.2012.13"                                                                                       
## [216] "IC2012_PY.Tuition.and.fees.2012.13..institutions.with.no.full.time..first.time..undergraduate.students."                            
## [217] "IC2012_PY.Books.and.supplies.2009.10"                                                                                               
## [218] "IC2012_PY.Books.and.supplies.2010.11"                                                                                               
## [219] "IC2012_PY.Books.and.supplies.2011.12"                                                                                               
## [220] "IC2012_PY.Books.and.supplies.2012.13"                                                                                               
## [221] "IC2012_PY.Books.and.supplies.2012.13..institutions.with.no.full.time..first.time..undergraduate.students."                          
## [222] "IC2012_PY.On.campus..room.and.board.2009.10"                                                                                        
## [223] "IC2012_PY.On.campus..room.and.board.2010.11"                                                                                        
## [224] "IC2012_PY.On.campus..room.and.board.2011.12"                                                                                        
## [225] "IC2012_PY.On.campus..room.and.board.2012.13"                                                                                        
## [226] "IC2012_PY.On.campus..other.expenses.2009.10"                                                                                        
## [227] "IC2012_PY.On.campus..other.expenses.2010.11"                                                                                        
## [228] "IC2012_PY.On.campus..other.expenses.2011.12"                                                                                        
## [229] "IC2012_PY.On.campus..other.expenses.2012.13"                                                                                        
## [230] "IC2012_PY.Off.campus..not.with.family...room.and.board.2009.10"                                                                     
## [231] "IC2012_PY.Off.campus..not.with.family...room.and.board.2010.11"                                                                     
## [232] "IC2012_PY.Off.campus..not.with.family...room.and.board.2011.12"                                                                     
## [233] "IC2012_PY.Off.campus..not.with.family...room.and.board.2012.13"                                                                     
## [234] "IC2012_PY.Off.campus..not.with.family...other.expenses.2009.10"                                                                     
## [235] "IC2012_PY.Off.campus..not.with.family...other.expenses.2010.11"                                                                     
## [236] "IC2012_PY.Off.campus..not.with.family...other.expenses.2011.12"                                                                     
## [237] "IC2012_PY.Off.campus..not.with.family...other.expenses.2012.13"                                                                     
## [238] "IC2012_PY.Off.campus..with.family...other.expenses.2009.10"                                                                         
## [239] "IC2012_PY.Off.campus..with.family...other.expenses.2010.11"                                                                         
## [240] "IC2012_PY.Off.campus..with.family...other.expenses.2011.12"                                                                         
## [241] "IC2012_PY.Off.campus..with.family...other.expenses.2012.13"                                                                         
## [242] "IC2012_PY.Comprehensive.fee.2009.10"                                                                                                
## [243] "IC2012_PY.Comprehensive.fee.2010.11"                                                                                                
## [244] "IC2012_PY.Comprehensive.fee.2011.12"                                                                                                
## [245] "IC2012_PY.Comprehensive.fee.2012.13"                                                                                                
## [246] "IC2012_PY.CIP.code.of.2nd.largest.program"                                                                                          
## [247] "IC2012_PY.Tuition.and.fees.of.2nd.largest.program"                                                                                  
## [248] "IC2012_PY.Cost.of.books.and.supplies.of.2nd.largest.program"                                                                        
## [249] "IC2012_PY.Length.of.2nd.largest.program"                                                                                            
## [250] "IC2012_PY.2nd.largest.program.measured.in.credit.or.contact.hours"                                                                  
## [251] "IC2012_PY.Number.of.months.to.complete.2nd.largest.program"                                                                         
## [252] "IC2012_PY.CIP.code.of.3rd.largest.program"                                                                                          
## [253] "IC2012_PY.Tuition.and.fees.of.3rd.largest.program"                                                                                  
## [254] "IC2012_PY.Cost.of.books.and.supplies.of.3rd.largest.program"                                                                        
## [255] "IC2012_PY.Length.of.3rd.largest.program"                                                                                            
## [256] "IC2012_PY.3rd.largest.program.measured.in.credit.or.contact.hours"                                                                  
## [257] "IC2012_PY.Number.of.months.to.complete.3rd.largest.program"                                                                         
## [258] "IC2012_PY.CIP.code.of.4th.largest.program"                                                                                          
## [259] "IC2012_PY.Tuition.and.fees.of.4th.largest.program"                                                                                  
## [260] "IC2012_PY.Cost.of.books.and.supplies.of.4th.largest.program"                                                                        
## [261] "IC2012_PY.Length.of.4th.largest.program"                                                                                            
## [262] "IC2012_PY.4th.largest.program.measured.in.credit.or.contact.hours"                                                                  
## [263] "IC2012_PY.Number.of.months.to.complete.4th.largest.program"                                                                         
## [264] "IC2012_PY.CIP.code.of.5th.largest.program"                                                                                          
## [265] "IC2012_PY.Tuition.and.fees.of.5th.largest.program"                                                                                  
## [266] "IC2012_PY.Cost.of.books.and.supplies.of.5th.largest.program"                                                                        
## [267] "IC2012_PY.Length.of.5th.largest.program"                                                                                            
## [268] "IC2012_PY.5th.largest.program.measured.in.credit.or.contact.hours"                                                                  
## [269] "IC2012_PY.Number.of.months.to.complete.5th.largest.program"                                                                         
## [270] "IC2012_PY.CIP.code.of.6th.largest.program"                                                                                          
## [271] "IC2012_PY.Tuition.and.fees.of.6th.largest.program"                                                                                  
## [272] "IC2012_PY.Cost.of.books.and.supplies.of.6th.largest.program"                                                                        
## [273] "IC2012_PY.Length.of.6th.largest.program"                                                                                            
## [274] "IC2012_PY.6th.largest.program.measured.in.credit.or.contact.hours"                                                                  
## [275] "IC2012_PY.Number.of.months.to.complete.6th.largest.program"                                                                         
## [276] "IC2012_AY.In.district.average.tuition.for.full.time.undergraduates"                                                                 
## [277] "IC2012_AY.In.district.required.fees.for.full.time.undergraduates"                                                                   
## [278] "IC2012_AY.In.district.per.credit.hour.charge.for.part.time.undergraduates"                                                          
## [279] "IC2012_AY.In.district.comprehensive.fee.for.full.time.undergraduates"                                                               
## [280] "IC2012_AY.In.state.average.tuition.for.full.time.undergraduates"                                                                    
## [281] "IC2012_AY.In.state.required.fees.for.full.time.undergraduates"                                                                      
## [282] "IC2012_AY.In.state.per.credit.hour.charge.for.part.time.undergraduates"                                                             
## [283] "IC2012_AY.In.state.comprehensive.fee.for.full.time.undergraduates"                                                                  
## [284] "IC2012_AY.Out.of.state.average.tuition.for.full.time.undergraduates"                                                                
## [285] "IC2012_AY.Out.of.state.required.fees.for.full.time.undergraduates"                                                                  
## [286] "IC2012_AY.Out.of.state.per.credit.hour.charge.for.part.time.undergraduates"                                                         
## [287] "IC2012_AY.Out.of.state.comprehensive.fee.for.full.time.undergraduates"                                                              
## [288] "IC2012_AY.In.district.average.tuition.full.time.graduates"                                                                          
## [289] "IC2012_AY.In.district.required.fees.for.full.time.graduates"                                                                        
## [290] "IC2012_AY.In.district.per.credit.hour.charge.part.time.graduates"                                                                   
## [291] "IC2012_AY.In.state.average.tuition.full.time.graduates"                                                                             
## [292] "IC2012_AY.In.state.required.fees.for.full.time.graduates"                                                                           
## [293] "IC2012_AY.In.state.per.credit.hour.charge.part.time.graduates"                                                                      
## [294] "IC2012_AY.Out.of.state.average.tuition.full.time.graduates"                                                                         
## [295] "IC2012_AY.Out.of.state.required.fees.for.full.time.graduates"                                                                       
## [296] "IC2012_AY.Out.of.state.per.credit.hour.charge.part.time.graduates"                                                                  
## [297] "IC2012_AY.Chiropractic..In.state.tuition"                                                                                           
## [298] "IC2012_AY.Chiropractic..In.state.required.fees"                                                                                     
## [299] "IC2012_AY.Chiropractic..Out.of.state.tuition"                                                                                       
## [300] "IC2012_AY.Chiropractic..Out.of.state.required.fees"                                                                                 
## [301] "IC2012_AY.Dentistry..In.state.tuition"                                                                                              
## [302] "IC2012_AY.Dentistry..In.state.required.fees"                                                                                        
## [303] "IC2012_AY.Dentistry..Out.of.state.tuition"                                                                                          
## [304] "IC2012_AY.Dentistry..Out.of.state.required.fees"                                                                                    
## [305] "IC2012_AY.Medicine..In.state.tuition"                                                                                               
## [306] "IC2012_AY.Medicine..In.state.required.fees"                                                                                         
## [307] "IC2012_AY.Medicine..Out.of.state.tuition"                                                                                           
## [308] "IC2012_AY.Medicine..Out.of.state.required.fees"                                                                                     
## [309] "IC2012_AY.Optometry..In.state.tuition"                                                                                              
## [310] "IC2012_AY.Optometry..In.state.required.fees"                                                                                        
## [311] "IC2012_AY.Optometry..Out.of.state.tuition"                                                                                          
## [312] "IC2012_AY.Optometry..Out.of.state.required.fees"                                                                                    
## [313] "IC2012_AY.Osteopathic.Medicine..In.state.tuition"                                                                                   
## [314] "IC2012_AY.Osteopathic.Medicine..In.state.required.fees"                                                                             
## [315] "IC2012_AY.Osteopathic.Medicine..Out.of.state.tuition"                                                                               
## [316] "IC2012_AY.Osteopathic.Medicine..Out.of.state.required.fees"                                                                         
## [317] "IC2012_AY.Pharmacy..In.state.tuition"                                                                                               
## [318] "IC2012_AY.Pharmacy..In.state.required.fees"                                                                                         
## [319] "IC2012_AY.Pharmacy..Out.of.state.tuition"                                                                                           
## [320] "IC2012_AY.Pharmacy..Out.of.state.required.fees"                                                                                     
## [321] "IC2012_AY.Podiatry..In.state.tuition"                                                                                               
## [322] "IC2012_AY.Podiatry..In.state.required.fees"                                                                                         
## [323] "IC2012_AY.Podiatry..Out.of.state.tuition"                                                                                           
## [324] "IC2012_AY.Podiatry..Out.of.state.required.fees"                                                                                     
## [325] "IC2012_AY.Veterinary.Medicine..In.state.tuition"                                                                                    
## [326] "IC2012_AY.Veterinary.Medicine..In.state.required.fees"                                                                              
## [327] "IC2012_AY.Veterinary.Medicine..Out.of.state.tuition"                                                                                
## [328] "IC2012_AY.Veterinary.Medicine..Out.of.state.required.fees"                                                                          
## [329] "IC2012_AY.Law..In.state.tuition"                                                                                                    
## [330] "IC2012_AY.Law..In.state.required.fees"                                                                                              
## [331] "IC2012_AY.Law..Out.of.state.tuition"                                                                                                
## [332] "IC2012_AY.Law..Out.of.state.required.fees"                                                                                          
## [333] "DRVIC2012.Total.price.for.in.district.students.living.on.campus..2012.13"                                                           
## [334] "DRVIC2012.Total.price.for.in.state.students.living.on.campus.2012.13"                                                               
## [335] "DRVIC2012.Total.price.for.out.of.state.students.living.on.campus.2012.13"                                                           
## [336] "DRVIC2012.Total.price.for.in.district.students.living.off.campus..not.with.family...2012.13"                                        
## [337] "DRVIC2012.Total.price.for.in.state.students.living.off.campus..not.with.family...2012.13"                                           
## [338] "DRVIC2012.Total.price.for.out.of.state.students.living.off.campus..not.with.family...2012.13"                                       
## [339] "DRVIC2012.Total.price.for.in.district.students.living.off.campus..with.family...2012.13"                                            
## [340] "DRVIC2012.Total.price.for.in.state.students.living.off.campus..with.family...2012.13"                                               
## [341] "DRVIC2012.Total.price.for.out.of.state.students.living.off.campus..with.family...2012.13"                                           
## [342] "IC2012_AY.Published.in.district.tuition.and.fees.2012.13"                                                                           
## [343] "IC2012_AY.Published.in.district.tuition.2012.13"                                                                                    
## [344] "IC2012_AY.Published.in.district.fees.2012.13"                                                                                       
## [345] "IC2012_AY.Published.in.district.tuition.2012.13.guaranteed.percent.increase..if.applicable."                                        
## [346] "IC2012_AY.Published.in.district.fees.2010.12.guaranteed.percent.increase..if.applicable."                                           
## [347] "IC2012_AY.Published.in.district.tuition.and.fees.2011.12"                                                                           
## [348] "IC2012_AY.Published.in.district.tuition.2011.12"                                                                                    
## [349] "IC2012_AY.Published.in.district.fees.2011.12"                                                                                       
## [350] "IC2012_AY.Published.in.district.tuition.and.fees.2010.11"                                                                           
## [351] "IC2012_AY.Published.in.district.tuition.2010.11"                                                                                    
## [352] "IC2012_AY.Published.in.district.fees.2010.11"                                                                                       
## [353] "IC2012_AY.Published.in.district.tuition.and.fees.2009.10"                                                                           
## [354] "IC2012_AY.Published.in.district.tuition.2009.10"                                                                                    
## [355] "IC2012_AY.Published.in.district.fees.2009.10"                                                                                       
## [356] "IC2012_AY.Published.in.state.tuition.and.fees.2012.13"                                                                              
## [357] "IC2012_AY.Published.in.state.tuition.2012.13"                                                                                       
## [358] "IC2012_AY.Published.in.state.fees.2012.13"                                                                                          
## [359] "IC2012_AY.Published.in.state.tuition.2010.12.guaranteed.percent.increase..if.applicable."                                           
## [360] "IC2012_AY.Published.in.state.fees.2010.12.guaranteed.percent.increase..if.applicable."                                              
## [361] "IC2012_AY.Published.in.state.tuition.and.fees.2011.12"                                                                              
## [362] "IC2012_AY.Published.in.state.tuition.2011.12"                                                                                       
## [363] "IC2012_AY.Published.in.state.fees.2011.12"                                                                                          
## [364] "IC2012_AY.Published.in.state.tuition.and.fees.2010.11"                                                                              
## [365] "IC2012_AY.Published.in.state.tuition.2010.11"                                                                                       
## [366] "IC2012_AY.Published.in.state.fees.2010.11"                                                                                          
## [367] "IC2012_AY.Published.in.state.tuition.and.fees.2009.10"                                                                              
## [368] "IC2012_AY.Published.in.state.tuition.2009.10"                                                                                       
## [369] "IC2012_AY.Published.in.state.fees.2009.10"                                                                                          
## [370] "IC2012_AY.Published.out.of.state.tuition.and.fees.2012.13"                                                                          
## [371] "IC2012_AY.Published.out.of.state.tuition.2012.13"                                                                                   
## [372] "IC2012_AY.Published.out.of.state.fees.2012.13"                                                                                      
## [373] "IC2012_AY.Published.out.of.state.tuition.2012.13.guaranteed.percent.increase..if.applicable."                                       
## [374] "IC2012_AY.Published.out.of.state.fees.2012.13.guaranteed.percent.increase..if.applicable."                                          
## [375] "IC2012_AY.Published.out.of.state.tuition.and.fees.2011.12"                                                                          
## [376] "IC2012_AY.Published.out.of.state.tuition.2011.12"                                                                                   
## [377] "IC2012_AY.Published.out.of.state.fees.2011.12"                                                                                      
## [378] "IC2012_AY.Published.out.of.state.tuition.and.fees.2010.11"                                                                          
## [379] "IC2012_AY.Published.out.of.state.tuition.2010.11"                                                                                   
## [380] "IC2012_AY.Published.out.of.state.fees.2010.11"                                                                                      
## [381] "IC2012_AY.Published.out.of.state.tuition.and.fees.2009.10"                                                                          
## [382] "IC2012_AY.Published.out.of.state.tuition.2009.10"                                                                                   
## [383] "IC2012_AY.Published.out.of.state.fees.2009.10"                                                                                      
## [384] "IC2012_AY.Books.and.supplies.2012.13"                                                                                               
## [385] "IC2012_AY.Books.and.supplies.2011.12"                                                                                               
## [386] "IC2012_AY.Books.and.supplies.2010.11"                                                                                               
## [387] "IC2012_AY.Books.and.supplies.2009.10"                                                                                               
## [388] "IC2012_AY.On.campus..room.and.board.2012.13"                                                                                        
## [389] "IC2012_AY.On.campus..room.and.board.2011.12"                                                                                        
## [390] "IC2012_AY.On.campus..room.and.board.2010.11"                                                                                        
## [391] "IC2012_AY.On.campus..room.and.board.2009.10"                                                                                        
## [392] "IC2012_AY.On.campus..other.expenses.2012.13"                                                                                        
## [393] "IC2012_AY.On.campus..other.expenses.2011.12"                                                                                        
## [394] "IC2012_AY.On.campus..other.expenses.2010.11"                                                                                        
## [395] "IC2012_AY.On.campus..other.expenses.2009.10"                                                                                        
## [396] "IC2012_AY.Off.campus..not.with.family...room.and.board.2012.13"                                                                     
## [397] "IC2012_AY.Off.campus..not.with.family...room.and.board.2011.12"                                                                     
## [398] "IC2012_AY.Off.campus..not.with.family...room.and.board.2010.11"                                                                     
## [399] "IC2012_AY.Off.campus..not.with.family...room.and.board.2009.10"                                                                     
## [400] "IC2012_AY.Off.campus..not.with.family...other.expenses.2012.13"                                                                     
## [401] "IC2012_AY.Off.campus..not.with.family...other.expenses.2011.12"                                                                     
## [402] "IC2012_AY.Off.campus..not.with.family...other.expenses.2010.11"                                                                     
## [403] "IC2012_AY.Off.campus..not.with.family...other.expenses.2009.10"                                                                     
## [404] "IC2012_AY.Off.campus..with.family...other.expenses.2012.13"                                                                         
## [405] "IC2012_AY.Off.campus..with.family...other.expenses.2011.12"                                                                         
## [406] "IC2012_AY.Off.campus..with.family...other.expenses.2010.11"                                                                         
## [407] "IC2012_AY.Off.campus..with.family...other.expenses.2009.10"                                                                         
## [408] "IC2012_AY.In.district.comprehensive.fee.2012.13"                                                                                    
## [409] "IC2012_AY.In.district.comprehensive.fee.2011.12.guaranteed.percent.increase"                                                        
## [410] "IC2012_AY.In.district.comprehensive.fee.2011.12"                                                                                    
## [411] "IC2012_AY.In.district.comprehensive.fee.2010.11"                                                                                    
## [412] "IC2012_AY.In.district.comprehensive.fee.2009.10"                                                                                    
## [413] "IC2012_AY.In.state.comprehensive.fee.2012.13"                                                                                       
## [414] "IC2012_AY.In.state.comprehensive.fee.2011.12.guaranteed.percent.increase"                                                           
## [415] "IC2012_AY.In.state.comprehensive.fee.2011.12"                                                                                       
## [416] "IC2012_AY.In.state.comprehensive.fee.2010.11"                                                                                       
## [417] "IC2012_AY.In.state.comprehensive.fee.2009.10"                                                                                       
## [418] "IC2012_AY.Out.of.state.comprehensive.fee.2012.13"                                                                                   
## [419] "IC2012_AY.Out.of.state.comprehensive.fee.2011.12.guaranteed.percent.increase"                                                       
## [420] "IC2012_AY.Out.of.state.comprehensive.fee.2011.12"                                                                                   
## [421] "IC2012_AY.Out.of.state.comprehensive.fee.2010.11"                                                                                   
## [422] "IC2012_AY.Out.of.state.comprehensive.fee.2009.10"                                                                                   
## [423] "IC2012.Member.of.National.Athletic.Association"                                                                                     
## [424] "IC2012.Member.of.National.Collegiate.Athletic.Association..NCAA."                                                                   
## [425] "IC2012.Member.of.National.Association.of.Intercollegiate.Athletics..NAIA."                                                          
## [426] "IC2012.Member.of.National.Junior.College.Athletic..Association..NJCAA."                                                             
## [427] "IC2012.Member.of.National.Small.College.Athletic.Association..NSCAA."                                                               
## [428] "IC2012.Member.of.National.Christian.College.Athletic.Association..NCCAA."                                                           
## [429] "IC2012.Member.of.other.national.athletic.association.not.listed.above"                                                              
## [430] "IC2012.NCAA.NAIA.member.for.football"                                                                                               
## [431] "IC2012.NCAA.NAIA.conference.number.football"                                                                                        
## [432] "IC2012.NCAA.NAIA.member.for.basketball"                                                                                             
## [433] "IC2012.NCAA.NAIA.conference.number.basketball"                                                                                      
## [434] "IC2012.NCAA.NAIA.member.for.baseball"                                                                                               
## [435] "IC2012.NCAA.NAIA.conference.number.baseball"                                                                                        
## [436] "IC2012.NCAA.NAIA.member.for.cross.country.track"                                                                                    
## [437] "IC2012.NCAA.NAIA.conference.number.cross.country.track"                                                                             
## [438] "IC2012MISSION.Mission.statement"                                                                                                    
## [439] "IC2012MISSION.Mission.statement.URL..if.mission.statement.not.provided."                                                            
## [440] "EFEST2012.Estimated.enrollment..total"                                                                                              
## [441] "EFEST2012.Estimated.enrollment..full.time"                                                                                          
## [442] "EFEST2012.Estimated.enrollment..part.time"                                                                                          
## [443] "EFEST2012.Estimated.undergraduate.enrollment..total"                                                                                
## [444] "EFEST2012.Estimated.undergraduate.enrollment..full.time"                                                                            
## [445] "EFEST2012.Estimated.undergraduate.enrollment..part.time"                                                                            
## [446] "EFEST2012.Estimated.first.time.degree.certificate.seeking.undergraduate.enrollment..total"                                          
## [447] "EFEST2012.Estimated.first.time.degree.certificate.seeking.undergraduate.enrollment..full.time"                                      
## [448] "EFEST2012.Estimated.first.time.degree.certificate.seeking.undergraduate.enrollment..part.time"                                      
## [449] "EFEST2012.Estimated.graduate.enrollment..total"                                                                                     
## [450] "EFEST2012.Estimated.graduate.enrollment..full.time"                                                                                 
## [451] "EFEST2012.Estimated.graduate.enrollment..part.time"                                                                                 
## [452] "IC2012.Percent.indicator.of.undergraduates.formally.registered.as.students.with.disabilities"                                       
## [453] "IC2012.Percent.of.undergraduates..who.are.formally.registered.as.students.with.disabilities..when.percentage.is.more.than.3.percent"
## [454] "CustomCGids2012.Institution.ID..IPEDSID..of.comparison.institution"                                                                 
## [455] "CustomCGids2012.Institution..entity..name.of.comparison.institution"                                                                
## [456] "CustomCGids2012.State.abbreviation.of.comparison.institution"
```

```r
str(df2)
```

```
## 'data.frame':	6280 obs. of  456 variables:
##  $ unitid                                                                                                                             : Factor w/ 391 levels "125231","142887",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ institution.name                                                                                                                   : Factor w/ 382 levels "Adrian College",..: 361 361 361 361 361 361 361 361 361 361 ...
##  $ year                                                                                                                               : int  2012 2012 2012 2012 2012 2012 2012 2012 2012 2012 ...
##  $ institution.name.1                                                                                                                 : Factor w/ 379 levels "","Adrian College",..: 358 358 358 358 358 358 358 358 358 358 ...
##  $ HD2012.Street.address.or.post.office.box                                                                                           : Factor w/ 378 levels "","020 Chubb Hall",..: 21 21 21 21 21 21 21 21 21 21 ...
##  $ HD2012.City.location.of.institution                                                                                                : Factor w/ 237 levels "","Ada","Addison",..: 135 135 135 135 135 135 135 135 135 135 ...
##  $ HD2012.State.abbreviation                                                                                                          : Factor w/ 8 levels "","Illinois",..: 6 6 6 6 6 6 6 6 6 6 ...
##  $ HD2012.ZIP.code                                                                                                                    : Factor w/ 373 levels "","43015-2370",..: 269 269 269 269 269 269 269 269 269 269 ...
##  $ HD2012.FIPS.state.code                                                                                                             : Factor w/ 8 levels "","Illinois",..: 6 6 6 6 6 6 6 6 6 6 ...
##  $ HD2012.Geographic.region                                                                                                           : Factor w/ 3 levels "","Great Lakes IL IN MI OH WI",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Name.of.chief.administrator                                                                                                 : Factor w/ 366 levels "","A. Charles Ware",..: 36 36 36 36 36 36 36 36 36 36 ...
##  $ HD2012.Title.of.chief.administrator                                                                                                : Factor w/ 30 levels "","Acting President",..: 18 18 18 18 18 18 18 18 18 18 ...
##  $ HD2012.General.information.telephone.number                                                                                        : num  8.01e+09 8.01e+09 8.01e+09 8.01e+09 8.01e+09 ...
##  $ HD2012.Fax.number                                                                                                                  : num  6.12e+09 6.12e+09 6.12e+09 6.12e+09 6.12e+09 ...
##  $ HD2012.Institution.s.internet.website.address                                                                                      : Factor w/ 356 levels "","awc.edu","go.cmich.edu",..: 337 337 337 337 337 337 337 337 337 337 ...
##  $ HD2012.Financial.aid.office.web.address                                                                                            : Factor w/ 319 levels "","admission.gustavus.edu/admissions/financialaid/default.asp",..: 304 304 304 304 304 304 304 304 304 304 ...
##  $ HD2012.Admissions.office.web.address                                                                                               : Factor w/ 318 levels "","67.222.6.109/~martin/admissions/",..: 303 303 303 303 303 303 303 303 303 303 ...
##  $ HD2012.Online.application.web.address                                                                                              : Factor w/ 296 levels "","admission.case.edu/apply/",..: 283 283 283 283 283 283 283 283 283 283 ...
##  $ HD2012.Net.price.calculator.web.address                                                                                            : Factor w/ 344 levels "","aaart.studentaidcalculator.com",..: 329 329 329 329 329 329 329 329 329 329 ...
##  $ HD2012.Office.of.Postsecondary.Education..OPE..ID.Number                                                                           : num  2504200 2504200 2504200 2504200 2504200 ...
##  $ HD2012.OPE.Title.IV.eligibility.indicator.code                                                                                     : Factor w/ 4 levels "","Deferment only - limited participation",..: 4 4 4 4 4 4 4 4 4 4 ...
##  $ HD2012.Employer.Identification.Number                                                                                              : num  6.5e+08 6.5e+08 6.5e+08 6.5e+08 6.5e+08 ...
##  $ HD2012.System..Governing.Board.or.Corporate.Structure                                                                              : Factor w/ 3 levels "","Institution is NOT part of a multi-institution or multi-campus organization",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Name.of.system..governing.board.or.corporate.entity.                                                                        : Factor w/ 39 levels "","Baker College System                                                            ",..: 23 23 23 23 23 23 23 23 23 23 ...
##  $ HD2012.Sector.of.institution                                                                                                       : Factor w/ 4 levels "","Private for-profit, 4-year or above",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Level.of.institution                                                                                                        : Factor w/ 2 levels "","Four or more years": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Control.of.institution                                                                                                      : Factor w/ 4 levels "","Private for-profit",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Highest.level.of.offering                                                                                                   : Factor w/ 6 levels "","Bachelor's degree",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Undergraduate.offering                                                                                                      : Factor w/ 2 levels "","Undergraduate degree or certificate offering": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Graduate.offering                                                                                                           : Factor w/ 3 levels "","Graduate degree or certificate offering",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Highest.degree.offered                                                                                                      : Factor w/ 7 levels "","Bachelor's degree",..: 5 5 5 5 5 5 5 5 5 5 ...
##  $ HD2012.Degree.granting.status                                                                                                      : Factor w/ 2 levels "","Degree-granting": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Historically.Black.College.or.University                                                                                    : Factor w/ 3 levels "","No","Yes": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Institution.has.hospital                                                                                                    : Factor w/ 4 levels "","No","Not applicable",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Institution.grants.a.medical.degree                                                                                         : Factor w/ 4 levels "","No","Not applicable",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Tribal.college                                                                                                              : Factor w/ 2 levels "","No": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Degree.of.urbanization..Urban.centric.locale.                                                                               : Factor w/ 13 levels "","City: Large",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Fips.County.code                                                                                                            : Factor w/ 177 levels "","Adams County, IL",..: 61 61 61 61 61 61 61 61 61 61 ...
##  $ HD2012.County.name                                                                                                                 : Factor w/ 149 levels "","Adams County",..: 53 53 53 53 53 53 53 53 53 53 ...
##  $ HD2012.Congressional.district.code                                                                                                 : Factor w/ 75 levels "","IA, District 01",..: 48 48 48 48 48 48 48 48 48 48 ...
##  $ HD2012.Core.Based.Statistical.Area..CBSA.                                                                                          : Factor w/ 121 levels "","Adrian, MI",..: 80 80 80 80 80 80 80 80 80 80 ...
##  $ HD2012.CBSA.Type.Metropolitan.or.Micropolitan                                                                                      : Factor w/ 4 levels "","Metropolitan Statistical Area",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Combined.Statistical.Area..CSA.                                                                                             : Factor w/ 49 levels "","Appleton-Oshkosh-Neenah, WI",..: 32 32 32 32 32 32 32 32 32 32 ...
##  $ HD2012.New.England.City.and.Town.Area..NECTA.                                                                                      : Factor w/ 2 levels "","Not applicable": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Longitude.location.of.institution                                                                                           : num  -93.3 -93.3 -93.3 -93.3 -93.3 ...
##  $ HD2012.Latitude.location.of.institution                                                                                            : num  45 45 45 45 45 ...
##  $ HD2012.Institution.open.to.the.general.public                                                                                      : Factor w/ 2 levels "","Institution is open to the public": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Status.of.institution                                                                                                       : Factor w/ 3 levels "","Active - institution active",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.UNITID.for.merged.schools                                                                                                   : int  -2 -2 -2 -2 -2 -2 -2 -2 -2 -2 ...
##  $ HD2012.Year.institution.was.deleted.from.IPEDS                                                                                     : Factor w/ 2 levels "","Not applicable": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Date.institution.closed                                                                                                     : num  -2 -2 -2 -2 -2 -2 -2 -2 -2 -2 ...
##  $ HD2012.Institution.is.active.in.current.year                                                                                       : Factor w/ 2 levels "","Yes": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Primarily.postsecondary.indicator                                                                                           : Factor w/ 2 levels "","Primarily postsecondary institution": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Postsecondary.institution.indicator                                                                                         : Factor w/ 2 levels "","Active postsecondary institution": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Postsecondary.and.Title.IV.institution.indicator                                                                            : Factor w/ 3 levels "","Non-Title IV postsecondary institution",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Reporting.method.for.student.charges..graduation.rates..retention.rates.and.student.financial.aid                           : Factor w/ 3 levels "","Student charges for full academic year and fall GR/SFA/retention rate cohort",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Institutional.category                                                                                                      : Factor w/ 2 levels "","Degree-granting, primarily baccalaureate or above": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Carnegie.Classification.2010..Basic                                                                                         : Factor w/ 18 levels "","Associate's--Private For-profit 4-year Primarily Associate's",..: 7 7 7 7 7 7 7 7 7 7 ...
##  $ HD2012.Carnegie.Classification.2010..Undergraduate.Instructional.Program                                                           : Factor w/ 20 levels "","Arts & sciences focus, high graduate coexistence",..: 15 15 15 15 15 15 15 15 15 15 ...
##  $ HD2012.Carnegie.Classification.2010..Graduate.Instructional.Program                                                                : Factor w/ 21 levels "","Comprehensive doctoral (no medical/veterinary)",..: 4 4 4 4 4 4 4 4 4 4 ...
##  $ HD2012.Carnegie.Classification.2010..Undergraduate.Profile                                                                         : Factor w/ 12 levels "","Full-time four-year, inclusive",..: 7 7 7 7 7 7 7 7 7 7 ...
##  $ HD2012.Carnegie.Classification.2010..Enrollment.Profile                                                                            : Factor w/ 7 levels "","Exclusively undergraduate four-year",..: 4 4 4 4 4 4 4 4 4 4 ...
##  $ HD2012.Carnegie.Classification.2010..Size.and.Setting                                                                              : Factor w/ 15 levels "","Large four-year, highly residential",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Land.Grant.Institution                                                                                                      : Factor w/ 3 levels "","Land Grant Institution",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ HD2012.Carnegie.Classification.2000                                                                                                : Factor w/ 17 levels "","{Item not available}",..: 8 8 8 8 8 8 8 8 8 8 ...
##  $ HD2012.Data.Feedback.Report.comparison.group.category.created.by.NCES                                                              : Factor w/ 79 levels "","Baccalaureate Colleges--Arts & Sciences or Diverse Fields, private for-profit /1 of 2",..: 59 59 59 59 59 59 59 59 59 59 ...
##  $ HD2012.Data.Feedback.Report...Institution.submitted.a..custom.comparison.group                                                     : Factor w/ 3 levels "","No, institution did not submit a custom comparison group",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ FLAGS2012.Status.of.IC.component.when.institution.was.migrated                                                                     : Factor w/ 2 levels "","Complete, final lock applied": 2 2 2 2 2 2 2 2 2 2 ...
##  $ FLAGS2012.Response.status....Institutional.characteristics.component                                                               : Factor w/ 2 levels "","Respondent": 2 2 2 2 2 2 2 2 2 2 ...
##  $ FLAGS2012.Type.of.imputation.method.Institutional.Characteristics                                                                  : Factor w/ 2 levels "","Not applicable": 2 2 2 2 2 2 2 2 2 2 ...
##  $ FLAGS2012.Natural.Disaster.identification                                                                                          : Factor w/ 2 levels "","No": 2 2 2 2 2 2 2 2 2 2 ...
##  $ HD2012.Institution.name.alias                                                                                                      : Factor w/ 143 levels "","AAC","AIU Online",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ IC2012.Occupational                                                                                                                : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Academic                                                                                                                    : Factor w/ 2 levels "","Yes": 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Continuing.professional                                                                                                     : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Recreational.or.avocational                                                                                                 : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Adult.basic.remedial.or.high.school.equivalent                                                                              : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Secondary..high.school.                                                                                                     : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Institutional.control.or.affiliation                                                                                        : Factor w/ 5 levels "","Private for-profit",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Primary.public.control                                                                                                      : Factor w/ 3 levels "","Not applicable",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Secondary.public.control                                                                                                    : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Religious.affiliation                                                                                                       : Factor w/ 38 levels "","African Methodist Episcopal",..: 26 26 26 26 26 26 26 26 26 26 ...
##  $ IC2012.Less.than.one.year.certificate                                                                                              : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.One.but.less.than.two.years.certificate                                                                                     : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Associate.s.degree                                                                                                          : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Two.but.less.than.4.years.certificate                                                                                       : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Bachelor.s.degree                                                                                                           : Factor w/ 2 levels "","Yes": 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Postbaccalaureate.certificate                                                                                               : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Master.s.degree                                                                                                             : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Post.master.s.certificate                                                                                                   : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Doctor.s.degree...research.scholarship                                                                                      : Factor w/ 3 levels "","Implied no",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Doctor.s.degree...professional.practice                                                                                     : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Doctor.s.degree...other                                                                                                     : Factor w/ 3 levels "","Implied no",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Other.degree                                                                                                                : Factor w/ 2 levels "","Implied no": 2 2 2 2 2 2 2 2 2 2 ...
##  $ IC2012.Open.admission.policy                                                                                                       : Factor w/ 3 levels "","No","Yes": 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Secondary.school.GPA                                                                                                        : Factor w/ 5 levels "","Neither required nor recommended",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Secondary.school.rank                                                                                                       : Factor w/ 5 levels "","Neither required nor recommended",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Secondary.school.record                                                                                                     : Factor w/ 5 levels "","Neither required nor recommended",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ IC2012.Completion.of.college.preparatory.program                                                                                   : Factor w/ 5 levels "","Neither required nor recommended",..: 3 3 3 3 3 3 3 3 3 3 ...
##   [list output truncated]
```



Category 3: Enrollments
---------------------------------------------


```r
df3_1 <- read.csv("2012/raw/03_Enrollments_1.csv")
dim(df3_1)
```

```
## [1] 1054   35
```

```r
names(df3_1)
```

```
##  [1] "unitid"                                                  
##  [2] "institution.name"                                        
##  [3] "year"                                                    
##  [4] "EFFY2012.Level.of.student"                               
##  [5] "EFFY2012.Grand.total"                                    
##  [6] "EFFY2012.Grand.total.men"                                
##  [7] "EFFY2012.Grand.total.women"                              
##  [8] "EFFY2012.American.Indian.or.Alaska.Native.total"         
##  [9] "EFFY2012.American.Indian.or.Alaska.Native.men"           
## [10] "EFFY2012.American.Indian.or.Alaska.Native.women"         
## [11] "EFFY2012.Asian.total"                                    
## [12] "EFFY2012.Asian.men"                                      
## [13] "EFFY2012.Asian.women"                                    
## [14] "EFFY2012.Black.or.African.American.total"                
## [15] "EFFY2012.Black.or.African.American.men"                  
## [16] "EFFY2012.Black.or.African.American.women"                
## [17] "EFFY2012.Hispanic.or.Latino.total"                       
## [18] "EFFY2012.Hispanic.or.Latino.men"                         
## [19] "EFFY2012.Hispanic.or.Latino.women"                       
## [20] "EFFY2012.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "EFFY2012.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "EFFY2012.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "EFFY2012.White.total"                                    
## [24] "EFFY2012.White.men"                                      
## [25] "EFFY2012.White.women"                                    
## [26] "EFFY2012.Two.or.more.races.total"                        
## [27] "EFFY2012.Two.or.more.races.men"                          
## [28] "EFFY2012.Two.or.more.races.women"                        
## [29] "EFFY2012.Race.ethnicity.unknown.total"                   
## [30] "EFFY2012.Race.ethnicity.unknown.men"                     
## [31] "EFFY2012.Race.ethnicity.unknown.women"                   
## [32] "EFFY2012.Nonresident.alien.total"                        
## [33] "EFFY2012.Nonresident.alien.men"                          
## [34] "EFFY2012.Nonresident.alien.women"                        
## [35] "IDX_E12"
```

```r
# str(df3_1)

df3_2 <- read.csv("2012/raw/03_Enrollments_2.csv")
dim(df3_2)
```

```
## [1] 3275   14
```

```r
names(df3_2)
```

```
##  [1] "unitid"                  "institution.name"       
##  [3] "year"                    "EF2012.Level.of.student"
##  [5] "EF2012.Grand.total"      "EF2012.Total.men"       
##  [7] "EF2012.Total.women"      "EF2012.Full.time.total" 
##  [9] "EF2012.Full.time.men"    "EF2012.Full.time.women" 
## [11] "EF2012.Part.time.total"  "EF2012.Part.time.men"   
## [13] "EF2012.Part.time.women"  "IDX_EF"
```

```r
# str(df3_2)

df3_3 <- read.csv("2012/raw/03_Enrollments_3.csv")
dim(df3_3)
```

```
## [1] 1761   14
```

```r
names(df3_3)
```

```
##  [1] "unitid"                                                                                                                                         
##  [2] "institution.name"                                                                                                                               
##  [3] "year"                                                                                                                                           
##  [4] "EF2012A_Dist.Level.of.student"                                                                                                                  
##  [5] "EF2012A_Dist.All.students.enrolled"                                                                                                             
##  [6] "EF2012A_Dist.Students.enrolled.exclusively.in.distance.education.courses"                                                                       
##  [7] "EF2012A_Dist.Students.enrolled.in.some.but.not.all.distance.education.courses"                                                                  
##  [8] "EF2012A_Dist.Student.not.enrolled.in.any.distance.education.courses"                                                                            
##  [9] "EF2012A_Dist.Students.enrolled.exclusively.in.distance.education.courses.and.are.located.in.same.state.jurisdiction.as.institution"             
## [10] "EF2012A_Dist.Students.enrolled.exclusively.in.distance.education.courses.and.are.located.in.U.S...not.in.same.state.jurisdiction.as.institution"
## [11] "EF2012A_Dist.Students.enrolled.exclusively.in.distance.education.courses.and.are.located.in.U.S...state.jurisdiction.unknown"                   
## [12] "EF2012A_Dist.Students.enrolled.exclusively.in.distance.education.courses.and.are.located.outside.U.S."                                          
## [13] "EF2012A_Dist.Students.enrolled.exclusively.in.distance.education.courses.and.location.of.student.unknown.not.reported"                          
## [14] "IDX_EF"
```

```r
# str(df3_3)

df3_4 <- read.csv("2012/raw/03_Enrollments_4.csv")
dim(df3_4)
```

```
## [1] 8191    7
```

```r
names(df3_4)
```

```
## [1] "unitid"                                                                                                                   
## [2] "institution.name"                                                                                                         
## [3] "year"                                                                                                                     
## [4] "EF2012C.State.of.residence.when.student.was.first.admitted"                                                               
## [5] "EF2012C.First.time.degree.certificate.seeking.undergraduate.students"                                                     
## [6] "EF2012C.First.time.degree.certificate.seeking.undergraduate.students.who.graduated.from.high.school.in.the.past.12.months"
## [7] "IDX_EF"
```

```r
# str(df3_4)

df3_5 <- read.csv("2012/raw/03_Enrollments_5.csv")
dim(df3_5)
```

```
## [1] 9401   35
```

```r
names(df3_5)
```

```
##  [1] "unitid"                                                 
##  [2] "institution.name"                                       
##  [3] "year"                                                   
##  [4] "EF2012A.Level.of.student"                               
##  [5] "EF2012A.Grand.total"                                    
##  [6] "EF2012A.Grand.total.men"                                
##  [7] "EF2012A.Grand.total.women"                              
##  [8] "EF2012A.American.Indian.or.Alaska.Native.total"         
##  [9] "EF2012A.American.Indian.or.Alaska.Native.men"           
## [10] "EF2012A.American.Indian.or.Alaska.Native.women"         
## [11] "EF2012A.Asian.total"                                    
## [12] "EF2012A.Asian.men"                                      
## [13] "EF2012A.Asian.women"                                    
## [14] "EF2012A.Black.or.African.American.total"                
## [15] "EF2012A.Black.or.African.American.men"                  
## [16] "EF2012A.Black.or.African.American.women"                
## [17] "EF2012A.Hispanic.total"                                 
## [18] "EF2012A.Hispanic.men"                                   
## [19] "EF2012A.Hispanic.women"                                 
## [20] "EF2012A.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "EF2012A.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "EF2012A.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "EF2012A.White.total"                                    
## [24] "EF2012A.White.men"                                      
## [25] "EF2012A.White.women"                                    
## [26] "EF2012A.Two.or.more.races.total"                        
## [27] "EF2012A.Two.or.more.races.men"                          
## [28] "EF2012A.Two.or.more.races.women"                        
## [29] "EF2012A.Race.ethnicity.unknown.total"                   
## [30] "EF2012A.Race.ethnicity.unknown.men"                     
## [31] "EF2012A.Race.ethnicity.unknown.women"                   
## [32] "EF2012A.Nonresident.alien.total"                        
## [33] "EF2012A.Nonresident.alien.men"                          
## [34] "EF2012A.Nonresident.alien.women"                        
## [35] "IDX_EF"
```

```r
# str(df3_5)

df3_6 <- read.csv("2012/raw/03_Enrollments_6.csv")
dim(df3_6)
```

```
## [1] 28646    35
```

```r
names(df3_6)
```

```
##  [1] "unitid"                                                  
##  [2] "institution.name"                                        
##  [3] "year"                                                    
##  [4] "EF2012CP.Major.field.of.study"                           
##  [5] "EF2012CP.Grand.total"                                    
##  [6] "EF2012CP.Total.men"                                      
##  [7] "EF2012CP.Total.women"                                    
##  [8] "EF2012CP.American.Indian.or.Alaska.Native.total"         
##  [9] "EF2012CP.American.Indian.or.Alaska.Native.men"           
## [10] "EF2012CP.American.Indian.or.Alaska.Native.women"         
## [11] "EF2012CP.Asian.total"                                    
## [12] "EF2012CP.Asian.men"                                      
## [13] "EF2012CP.Asian.women"                                    
## [14] "EF2012CP.Black.or.African.American.total"                
## [15] "EF2012CP.Black.or.African.American.men"                  
## [16] "EF2012CP.Black.or.African.American.women"                
## [17] "EF2012CP.Hispanic.total"                                 
## [18] "EF2012CP.Hispanic.men"                                   
## [19] "EF2012CP.Hispanic.women"                                 
## [20] "EF2012CP.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "EF2012CP.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "EF2012CP.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "EF2012CP.White.total"                                    
## [24] "EF2012CP.White.men"                                      
## [25] "EF2012CP.White.women"                                    
## [26] "EF2012CP.Two.or.more.races.total"                        
## [27] "EF2012CP.Two.or.more.races.men"                          
## [28] "EF2012CP.Two.or.more.races.women"                        
## [29] "EF2012CP.Race.ethnicity.unknown.total"                   
## [30] "EF2012CP.Race.ethnicity.unknown.men"                     
## [31] "EF2012CP.Race.ethnicity.unknown.women"                   
## [32] "EF2012CP.Nonresident.alien.total"                        
## [33] "EF2012CP.Nonresident.alien.men"                          
## [34] "EF2012CP.Nonresident.alien.women"                        
## [35] "IDX_EF"
```

```r
# str(df3_6)

df3_7 <- read.csv("2012/raw/03_Enrollments_7.csv")
dim(df3_7)
```

```
## [1] 8336   15
```

```r
names(df3_7)
```

```
##  [1] "unitid"                   "institution.name"        
##  [3] "year"                     "EF2012B.Age.category"    
##  [5] "EF2012B.Level.of.student" "EF2012B.Grand.total"     
##  [7] "EF2012B.Total.men"        "EF2012B.Total.women"     
##  [9] "EF2012B.Full.time.total"  "EF2012B.Full.time.men"   
## [11] "EF2012B.Full.time.women"  "EF2012B.Part.time.total" 
## [13] "EF2012B.Part.time.men"    "EF2012B.Part.time.women" 
## [15] "IDX_EF"
```

```r
# str(df3_7)

df3_8 <- read.csv("2012/raw/03_Enrollments_8.csv")
dim(df3_8)
```

```
## [1] 380 148
```

```r
names(df3_8)
```

```
##   [1] "unitid"                                                                                                                             
##   [2] "institution.name"                                                                                                                   
##   [3] "year"                                                                                                                               
##   [4] "FLAGS2012.Natural.Disaster.identification"                                                                                          
##   [5] "FLAGS2012.Response.status.of.institution....Fall.enrollment"                                                                        
##   [6] "FLAGS2012.Status.of.Fall.Enrollment.survey.when.data.collection.closed"                                                             
##   [7] "FLAGS2012.Parent.child.indicator.f..Fall.enrollment"                                                                                
##   [8] "FLAGS2012.ID.number.of.parent.institution...Fall.enrollment"                                                                        
##   [9] "FLAGS2012.Parent.child.allocation.factor...Fall.enrollment"                                                                         
##  [10] "FLAGS2012.Type.of.imputation.method...Fall.enrollment"                                                                              
##  [11] "FLAGS2012.Status.enrollment.by.race.ethnicity..99.0000.CIP."                                                                        
##  [12] "FLAGS2012.Status.enrollment.by.major"                                                                                               
##  [13] "FLAGS2012.Status.enrollment.summary.by.age"                                                                                         
##  [14] "FLAGS2012.Status.residence.of.first.time.first.year.students"                                                                       
##  [15] "FLAGS2012.Status.total.entering.class.and.retention.rates"                                                                          
##  [16] "EF2012D.Full.time.first.time.degree.certificate.seeking.undergraduate..current.year.GRS.cohort."                                    
##  [17] "EF2012D.Total.entering.students.at.the.undergraduate.level..fall.2012"                                                              
##  [18] "EF2012D.Current.year.GRS.cohort.as.a.percent.of.entering.class"                                                                     
##  [19] "EFIA2012.12.month.instructional.activity.credit.hours..undergraduates"                                                              
##  [20] "EFIA2012.12.month.instructional.activity.contact.hours..undergraduates"                                                             
##  [21] "EFIA2012.12.month.instructional.activity.credit.hours..graduates"                                                                   
##  [22] "EFIA2012.Estimated.full.time.equivalent..FTE..undergraduate.enrollment..2011.12"                                                    
##  [23] "EFIA2012.Estimated.full.time.equivalent..FTE..graduate.enrollment..2011.12"                                                         
##  [24] "EFIA2012.Reported.full.time.equivalent..FTE..undergraduate.enrollment..2011.12"                                                     
##  [25] "EFIA2012.Reported.full.time.equivalent..FTE..graduate.enrollment..2011.12"                                                          
##  [26] "EFIA2012.Reported.full.time.equivalent..FTE..doctor.s.professional.practice..2011.12"                                               
##  [27] "EFIA2012.Is.instructional.activity.based.on.credit.or.contact.hours"                                                                
##  [28] "EF2012D.Full.time.fall.2011.cohort"                                                                                                 
##  [29] "EF2012D.Exclusions.from.full.time.fall.2011.cohort"                                                                                 
##  [30] "EF2012D.Full.time.adjusted.fall.2011.cohort"                                                                                        
##  [31] "EF2012D.Students.from.the.full.time.adjusted.fall.2011.cohort.enrolled.in.fall.2012"                                                
##  [32] "EF2012D.Full.time.retention.rate..2012"                                                                                             
##  [33] "EF2012D.Part.time.fall.2011.cohort"                                                                                                 
##  [34] "EF2012D.Exclusions.from.part.time.fall.2011.cohort"                                                                                 
##  [35] "EF2012D.Part.time.adjusted.fall.2011.cohort"                                                                                        
##  [36] "EF2012D.Students.from.the.part.time.adjusted.fall.2011.cohort.enrolled.in.fall.2012"                                                
##  [37] "EF2012D.Part.time.retention.rate..2012"                                                                                             
##  [38] "HD2012.Institution.size.category"                                                                                                   
##  [39] "DRVEF2012.Total..enrollment"                                                                                                        
##  [40] "DRVEF2012.Full.time.enrollment"                                                                                                     
##  [41] "DRVEF2012.Part.time.enrollment"                                                                                                     
##  [42] "DRVEF2012.Full.time.equivalent.fall.enrollment"                                                                                     
##  [43] "DRVEF2012.Undergraduate.enrollment"                                                                                                 
##  [44] "DRVEF2012.First.time.degree.certificate.seeking.undergraduate.enrollment"                                                           
##  [45] "DRVEF2012.Transfer.in.degree.certificate.seeking.undergraduate.enrollment"                                                          
##  [46] "DRVEF2012.Continuing.degree.certificate.seeking.undergraduate.enrollment"                                                           
##  [47] "DRVEF2012.Nondegree.certificate.seeking.undergraduate.enrollment"                                                                   
##  [48] "DRVEF2012.Graduate.enrollment"                                                                                                      
##  [49] "DRVEF2012.Full.time.undergraduate.enrollment"                                                                                       
##  [50] "DRVEF2012.Full.time.first.time.degree.certificate.seeking.undergraduate.enrollment"                                                 
##  [51] "DRVEF2012.Full.time.transfer.in.degree.certificate.seeking.undergraduate.enrollment"                                                
##  [52] "DRVEF2012.Full.time.continuing.degree.certificate.seeking.undergraduate.enrollment"                                                 
##  [53] "DRVEF2012.Full.time.nondegree.certificate.seeking.undergraduate.enrollment"                                                         
##  [54] "DRVEF2012.Full.time.graduate.enrollment"                                                                                            
##  [55] "DRVEF2012.Part.time.undergraduate.enrollment"                                                                                       
##  [56] "DRVEF2012.Part.time.first.time.degree.certificate.seeking.undergraduate.enrollment"                                                 
##  [57] "DRVEF2012.Part.time.transfer.in.degree.certificate.seeking.undergraduate.enrollment"                                                
##  [58] "DRVEF2012.Part.time.continuing.degree.certificate.seeking.undergraduate.enrollment"                                                 
##  [59] "DRVEF2012.Part.time.nondegree.certificate.seeking.undergraduate.enrollment"                                                         
##  [60] "DRVEF2012.Part.time.graduate.enrollment"                                                                                            
##  [61] "DRVEF2012.Percent.of.total.enrollment.that.are.American.Indian.or.Alaska.Native"                                                    
##  [62] "DRVEF2012.Percent.of.total.enrollment.that.are.Asian"                                                                               
##  [63] "DRVEF2012.Percent.of.total.enrollment.that.are.Black.or.African.American"                                                           
##  [64] "DRVEF2012.Percent.of.total.enrollment.that.are.Hispanic.Latino"                                                                     
##  [65] "DRVEF2012.Percent.of.total.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander"                                           
##  [66] "DRVEF2012.Percent.of.total.enrollment.that.are.White"                                                                               
##  [67] "DRVEF2012.Percent.of.total.enrollment.that.are.two.or.more.races"                                                                   
##  [68] "DRVEF2012.Percent.of.total.enrollment.that.are.Race.ethnicity.unknown"                                                              
##  [69] "DRVEF2012.Percent.of.total.enrollment.that.are.Nonresident.Alien"                                                                   
##  [70] "DRVEF2012.Percent.of.total.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander"                                              
##  [71] "DRVEF2012.Percent.of.total.enrollment.that.are.women"                                                                               
##  [72] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.American.Indian.or.Alaska.Native"                                            
##  [73] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Asian"                                                                       
##  [74] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Black.or.African.American"                                                   
##  [75] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Hispanic.Latino"                                                             
##  [76] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander"                                   
##  [77] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.White"                                                                       
##  [78] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.two.or.more.races"                                                           
##  [79] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Race.ethnicity.unknown"                                                      
##  [80] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Nonresident.Alien"                                                           
##  [81] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander"                                      
##  [82] "DRVEF2012.Percent.of.undergraduate.enrollment.that.are.women"                                                                       
##  [83] "DRVEF2012.Percent.of.graduate.enrollment.that.are.American.Indian.or.Alaska.Native"                                                 
##  [84] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Asian"                                                                            
##  [85] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Black.or.African.American"                                                        
##  [86] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Hispanic.Latino"                                                                  
##  [87] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Native.Hawaiian.or.Other.Pacific.Islander"                                        
##  [88] "DRVEF2012.Percent.of.graduate.enrollment.that.are.White"                                                                            
##  [89] "DRVEF2012.Percent.of.graduate.enrollment.that.are.two.or.more.races"                                                                
##  [90] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Race.ethnicity.unknown"                                                           
##  [91] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Nonresident.Alien"                                                                
##  [92] "DRVEF2012.Percent.of.graduate.enrollment.that.are.Asian.Native.Hawaiian.Pacific.Islander"                                           
##  [93] "DRVEF2012.Percent.of.graduate.enrollment.that.are.women"                                                                            
##  [94] "DRVEF2012.Full.time..first.time..degree.certificate.seeking.undergraduates..GRS.Cohort..as.percent.of.all.undergraduates"           
##  [95] "DRVEF2012.Adult.age..25.64..enrollment..all.students"                                                                               
##  [96] "DRVEF2012.Adult.age..25.64..enrollment..undergraduate"                                                                              
##  [97] "DRVEF2012.Adult.age..25.64..enrollment..graduate"                                                                                   
##  [98] "DRVEF2012.Adult.age..25.64..enrollment..full.time.students"                                                                         
##  [99] "DRVEF2012.Adult.age..25.64..enrollment..full.time.undergraduate"                                                                    
## [100] "DRVEF2012.Adult.age..25.64..enrollment..full.time.graduate"                                                                         
## [101] "DRVEF2012.Adult.age..25.64..enrollment..part.time.students"                                                                         
## [102] "DRVEF2012.Adult.age..25.64..enrollment..part.time.undergraduate"                                                                    
## [103] "DRVEF2012.Adult.age..25.64..enrollment..part.time.graduate"                                                                         
## [104] "DRVEF2012.Percent.of.undergraduate.enrollment.under.18"                                                                             
## [105] "DRVEF2012.Percent.of.undergraduate.enrollment.18.24"                                                                                
## [106] "DRVEF2012.Percent.of.undergraduate.enrollment..25.64"                                                                               
## [107] "DRVEF2012.Percent.of.undergraduate.enrollment.over.65"                                                                              
## [108] "DRVEF_RM2012.Number.of.first.time.undergraduates...in.state"                                                                        
## [109] "DRVEF_RM2012.Percent.of.first.time.undergraduates...in.state"                                                                       
## [110] "DRVEF_RM2012.Number.of.first.time.undergraduates...out.of.state"                                                                    
## [111] "DRVEF_RM2012.Percent.of.first.time.undergraduates...out.of.state"                                                                   
## [112] "DRVEF_RM2012.Number.of.first.time.undergraduates...foreign.countries"                                                               
## [113] "DRVEF_RM2012.Percent.of.first.time.undergraduates...foreign.countries"                                                              
## [114] "DRVEF_RM2012.Number.of.first.time.undergraduates...residence.unknown"                                                               
## [115] "DRVEF_RM2012.Percent.of.first.time.undergraduates...residence.unknown"                                                              
## [116] "DRVEFDE2012.Percent.of.students.enrolled.exclusively.in.distance.education.courses"                                                 
## [117] "DRVEFDE2012.Percent.of.students.enrolled.in.some.but.not.all.distance.education.courses"                                            
## [118] "DRVEFDE2012.Percent.of.students.not.enrolled.in.any.distance.education.courses"                                                     
## [119] "DRVEFDE2012.Percent.of.undergraduate.students.enrolled.exclusively.in.distance.education.courses"                                   
## [120] "DRVEFDE2012.Percent.of.undergraduate.students.enrolled.in.some.but.not.all.distance.education.courses"                              
## [121] "DRVEFDE2012.Percent.of.undergraduate.students.not.enrolled.in.any.distance.education.courses"                                       
## [122] "DRVEFDE2012.Percent.of.graduate.students.enrolled.exclusively.in.distance.education.courses"                                        
## [123] "DRVEFDE2012.Percent.of.graduate.students.enrolled.in.some.but.not.all.distance.education.courses"                                   
## [124] "DRVEFDE2012.Percent.of.graduate.students.not.enrolled.in.any.distance.education.courses"                                            
## [125] "DRVEF122012.12.month.unduplicated.headcount..total..2011.12"                                                                        
## [126] "DRVEF122012.12.month.unduplicated.headcount..undergraduate..2011.12"                                                                
## [127] "DRVEF122012.12.month.full.time.equivalent.enrollment..2011.12"                                                                      
## [128] "EFEST2012.Estimated.enrollment..total"                                                                                              
## [129] "EFEST2012.Estimated.enrollment..full.time"                                                                                          
## [130] "EFEST2012.Estimated.enrollment..part.time"                                                                                          
## [131] "EFEST2012.Estimated.undergraduate.enrollment..total"                                                                                
## [132] "EFEST2012.Estimated.undergraduate.enrollment..full.time"                                                                            
## [133] "EFEST2012.Estimated.undergraduate.enrollment..part.time"                                                                            
## [134] "EFEST2012.Estimated.first.time.degree.certificate.seeking.undergraduate.enrollment..total"                                          
## [135] "EFEST2012.Estimated.first.time.degree.certificate.seeking.undergraduate.enrollment..full.time"                                      
## [136] "EFEST2012.Estimated.first.time.degree.certificate.seeking.undergraduate.enrollment..part.time"                                      
## [137] "EFEST2012.Estimated.graduate.enrollment..total"                                                                                     
## [138] "EFEST2012.Estimated.graduate.enrollment..full.time"                                                                                 
## [139] "EFEST2012.Estimated.graduate.enrollment..part.time"                                                                                 
## [140] "FLAGS2012.Response.status.of.institution...12.month.enrollment"                                                                     
## [141] "FLAGS2012.Status.of.12.month.enrollment.component.whe.data.collection.closed"                                                       
## [142] "FLAGS2012.Parent.child.indicator.for.12.month.enrollment"                                                                           
## [143] "FLAGS2012.ID.number.of.parent.institution...12.month.enrollment"                                                                    
## [144] "FLAGS2012.Parent.child.allocation.factor...12.month.enrollment"                                                                     
## [145] "FLAGS2012.Type.of.imputation.method...12.month.enrollment"                                                                          
## [146] "EF2012D.Student.to.faculty.ratio"                                                                                                   
## [147] "IC2012.Percent.indicator.of.undergraduates.formally.registered.as.students.with.disabilities"                                       
## [148] "IC2012.Percent.of.undergraduates..who.are.formally.registered.as.students.with.disabilities..when.percentage.is.more.than.3.percent"
```

```r
# str(df3_8)
```


Category 4: Completions
-----------------------


```r
df4_1 <- read.csv("2012/raw/04_Completions_1.csv")
dim(df4_1)
```

```
## [1] 20047    30
```

```r
names(df4_1)
```

```
##  [1] "unitid"                                                                                             
##  [2] "institution.name"                                                                                   
##  [3] "year"                                                                                               
##  [4] "C2012DEP.CIPCODE"                                                                                   
##  [5] "CipTitle"                                                                                           
##  [6] "C2012DEP.Number.of.programs.offered"                                                                
##  [7] "C2012DEP.Number.of.programs.offered.via.distance.education"                                         
##  [8] "C2012DEP.Number.of.Associate.s.degree.programs.offered"                                             
##  [9] "C2012DEP.Number.of.Associate.s.degree.programs.offered.via.distance.education"                      
## [10] "C2012DEP.Number.of.Bachelor.s.degree.programs.offered"                                              
## [11] "C2012DEP.Number.of.Bachelor.s.degree.programs.offered.via.distance.education"                       
## [12] "C2012DEP.Number.of.Master.s.degree.programs.offered"                                                
## [13] "C2012DEP.Number.of.Master.s.degree.programs.offered.via.distance.education"                         
## [14] "C2012DEP.Number.of.Doctor.s.degree.research.scholarship.programs.offered"                           
## [15] "C2012DEP.Number.of.Doctor.s.degree.research.scholarship.programs.offered.via.distance.education"    
## [16] "C2012DEP.Number.of.Doctor.s.degree.professional.practice.programs.offered"                          
## [17] "C2012DEP.Number.of.Doctor.s.degree.professional.practice.programs.offered.via.distance.education"   
## [18] "C2012DEP.Number.of.Doctor.s.degree.other.programs.offered"                                          
## [19] "C2012DEP.Number.of.Doctor.s.degree.other.programs.offered.via.distance.education"                   
## [20] "C2012DEP.Number.of.less.than.1.year.certificate.programs.offered"                                   
## [21] "C2012DEP.Number.of.less.than.1.year.certificate.programs.offered.via.distance.education"            
## [22] "C2012DEP.Number.of.1.year..but.less.than.2.year.certificate.programs.offered"                       
## [23] "C2012DEP.Number.of.1.year..but.less.than.2.year.certificate.programs.offered.via.distance.education"
## [24] "C2012DEP.Number.of.2.year..but.less.than.4.year.certificate.programs.offered"                       
## [25] "C2012DEP.Number.of.2.year..but.less.than.4.year.certificate.programs.offered.via.distance.education"
## [26] "C2012DEP.Number.of.Postbaccalaureate.certificate.programs.offered"                                  
## [27] "C2012DEP.Number.of.Postbaccalaureate.certificate.programs.offered.via.distance.education"           
## [28] "C2012DEP.Number.of.Post.master.s.certificate.programs.offered"                                      
## [29] "C2012DEP.Number.of.Post.master.s.certificate.programs.offered.via.distance.education"               
## [30] "IDX_C"
```

```r
# str(df4_1)

df4_2 <- read.csv("2012/raw/04_Completions_2.csv")
dim(df4_2)
```

```
## [1] 1182   22
```

```r
names(df4_2)
```

```
##  [1] "unitid"                                                 
##  [2] "institution.name"                                       
##  [3] "year"                                                   
##  [4] "C2012_C.Award.Level.code"                               
##  [5] "C2012_C.Grand.total"                                    
##  [6] "C2012_C.Grant.total.men"                                
##  [7] "C2012_C.Grand.total.women"                              
##  [8] "C2012_C.American.Indian.or.Alaska.Native.total"         
##  [9] "C2012_C.Asian.total"                                    
## [10] "C2012_C.Black.or.African.American.total"                
## [11] "C2012_C.Hispanic.or.Latino.total"                       
## [12] "C2012_C.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [13] "C2012_C.White.total"                                    
## [14] "C2012_C.Two.or.more.races.total"                        
## [15] "C2012_C.Race.ethnicity.unknown.total"                   
## [16] "C2012_C.Nonresident.alien.total"                        
## [17] "C2012_C.Ages..under.18"                                 
## [18] "C2012_C.Ages..18.24"                                    
## [19] "C2012_C.Ages..25.39"                                    
## [20] "C2012_C.Ages..40.and.above"                             
## [21] "C2012_C.Age.unknown"                                    
## [22] "IDX_C"
```

```r
# str(df4_2)

df4_3 <- read.csv("2012/raw/04_Completions_3.csv")
dim(df4_3)
```

```
## [1] 36739    39
```

```r
names(df4_3)
```

```
##  [1] "unitid"                                                 
##  [2] "institution.name"                                       
##  [3] "year"                                                   
##  [4] "C2012_A.First.or.Second.Major"                          
##  [5] "C2012_A.CIP.Code....2010.Classification"                
##  [6] "CipTitle"                                               
##  [7] "C2012_A.Award.Level.code"                               
##  [8] "C2012_A.Program.offered.as.a.distance.education.program"
##  [9] "C2012_A.Grand.total"                                    
## [10] "C2012_A.Grand.total.men"                                
## [11] "C2012_A.Grand.total.women"                              
## [12] "C2012_A.American.Indian.or.Alaska.Native.total"         
## [13] "C2012_A.American.Indian.or.Alaska.Native.men"           
## [14] "C2012_A.American.Indian.or.Alaska.Native.women"         
## [15] "C2012_A.Asian.total"                                    
## [16] "C2012_A.Asian.men"                                      
## [17] "C2012_A.Asian.women"                                    
## [18] "C2012_A.Black.or.African.American.total"                
## [19] "C2012_A.Black.or.African.American.men"                  
## [20] "C2012_A.Black.or.African.American.women"                
## [21] "C2012_A.Hispanic.or.Latino.total"                       
## [22] "C2012_A.Hispanic.or.Latino.men"                         
## [23] "C2012_A.Hispanic.or.Latino.women"                       
## [24] "C2012_A.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [25] "C2012_A.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [26] "C2012_A.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [27] "C2012_A.White.total"                                    
## [28] "C2012_A.White.men"                                      
## [29] "C2012_A.White.women"                                    
## [30] "C2012_A.Two.or.more.races.total"                        
## [31] "C2012_A.Two.or.more.races.men"                          
## [32] "C2012_A.Two.or.more.races.women"                        
## [33] "C2012_A.Race.ethnicity.unknown.total"                   
## [34] "C2012_A.Race.ethnicity.unknown.men"                     
## [35] "C2012_A.Race.ethnicity.unknown.women"                   
## [36] "C2012_A.Nonresident.alien.total"                        
## [37] "C2012_A.Nonresident.alien.men"                          
## [38] "C2012_A.Nonresident.alien.women"                        
## [39] "IDX_C"
```

```r
# str(df4_3)

df4_4 <- read.csv("2012/raw/04_Completions_4.csv")
dim(df4_4)
```

```
## [1] 380  57
```

```r
names(df4_4)
```

```
##  [1] "unitid"                                                                                
##  [2] "institution.name"                                                                      
##  [3] "year"                                                                                  
##  [4] "FLAGS2012.Response.status....Completions.component"                                    
##  [5] "FLAGS2012.Status.of.completions.component.when.institution.was.migrated"               
##  [6] "FLAGS2012.Parent.child.indicator.for.completions"                                      
##  [7] "FLAGS2012.UnitID.of.Parent.institution"                                                
##  [8] "FLAGS2012.Parent.child.allocation.factor...Completions"                                
##  [9] "FLAGS2012.Type.of.imputation.method.Completions"                                       
## [10] "DRVC2012.Associate.s.degree"                                                           
## [11] "DRVC2012.Bachelor.s.degree"                                                            
## [12] "DRVC2012.Master.s.degree"                                                              
## [13] "DRVC2012.Doctor.s.degree...research.scholarship"                                       
## [14] "DRVC2012.Doctor.s.degree...professional.practice"                                      
## [15] "DRVC2012.Doctor.s.degree...other"                                                      
## [16] "DRVC2012.Certificates.of.less.than.1.year"                                             
## [17] "DRVC2012.Certificates.of.1.but.less.than.2.years"                                      
## [18] "DRVC2012.Certificates.of.2.but.less.than.4.years"                                      
## [19] "DRVC2012.Postbaccalaureate.certificates"                                               
## [20] "DRVC2012.Post.master.s.certificates"                                                   
## [21] "DRVC2012.Number.of.students.receiving.an.Associate.s.degree"                           
## [22] "DRVC2012.Number.of.students.receiving.a.Bachelor.s.degree"                             
## [23] "DRVC2012.Number.of.students.receiving.a.Master.s.degree"                               
## [24] "DRVC2012.Number.of.students.receiving.a.Doctor.s.degree"                               
## [25] "DRVC2012.Number.of.students.receiving.a.certificate.of.less.than.1.year"               
## [26] "DRVC2012.Number.of.students.receiving.a.certificate.of.1.but.less.than.4.years"        
## [27] "DRVC2012.Number.of.students.receiving.a.Postbaccalaureate.or.Post.master.s.certificate"
## [28] "C2012_B.Grand.total"                                                                   
## [29] "C2012_B.Grand.total.men"                                                               
## [30] "C2012_B.Grand.total.women"                                                             
## [31] "C2012_B.American.Indian.or.Alaska.Native.total"                                        
## [32] "C2012_B.American.Indian.or.Alaska.Native.men"                                          
## [33] "C2012_B.American.Indian.or.Alaska.Native.women"                                        
## [34] "C2012_B.Asian.total"                                                                   
## [35] "C2012_B.Asian.men"                                                                     
## [36] "C2012_B.Asian.women"                                                                   
## [37] "C2012_B.Black.or.African.American.total"                                               
## [38] "C2012_B.Black.or.African.American.men"                                                 
## [39] "C2012_B.Black.or.African.American.women"                                               
## [40] "C2012_B.Hispanic.or.Latino.total"                                                      
## [41] "C2012_B.Hispanic.or.Latino.men"                                                        
## [42] "C2012_B.Hispanic.or.Latino.women"                                                      
## [43] "C2012_B.Native.Hawaiian.or.Other.Pacific.Islander.total"                               
## [44] "C2012_B.Native.Hawaiian.or.Other.Pacific.Islander.men"                                 
## [45] "C2012_B.Native.Hawaiian.or.Other.Pacific.Islander.women"                               
## [46] "C2012_B.White.total"                                                                   
## [47] "C2012_B.White.men"                                                                     
## [48] "C2012_B.White.women"                                                                   
## [49] "C2012_B.Two.or.more.races.total"                                                       
## [50] "C2012_B.Two.or.more.races.men"                                                         
## [51] "C2012_B.Two.or.more.races.women"                                                       
## [52] "C2012_B.Race.ethnicity.unknown.total"                                                  
## [53] "C2012_B.Race.ethnicity.unknown.men"                                                    
## [54] "C2012_B.Race.ethnicity.unknown.women"                                                  
## [55] "C2012_B.Nonresident.alien.total"                                                       
## [56] "C2012_B.Nonresident.alien.men"                                                         
## [57] "C2012_B.Nonresident.alien.women"
```

```r
# str(df4_4)
```


Category 5: Graduation rates
----------------------------


```r
df5_1 <- read.csv("2012/raw/05_Graduation_rates_1.csv")
dim(df5_1)
```

```
## [1] 5322   35
```

```r
names(df5_1)
```

```
##  [1] "unitid"                                                
##  [2] "institution.name"                                      
##  [3] "year"                                                  
##  [4] "GR2012.Cohort.data"                                    
##  [5] "GR2012.Grand.total"                                    
##  [6] "GR2012.Total.men"                                      
##  [7] "GR2012.Total.women"                                    
##  [8] "GR2012.American.Indian.or.Alaska.Native.total"         
##  [9] "GR2012.American.Indian.or.Alaska.Native.men"           
## [10] "GR2012.American.Indian.or.Alaska.Native.women"         
## [11] "GR2012.Asian.total"                                    
## [12] "GR2012.Asian.women"                                    
## [13] "GR2012.Asian.men"                                      
## [14] "GR2012.Black.or.African.American.total"                
## [15] "GR2012.Black.or.African.American.men"                  
## [16] "GR2012.Black.or.African.American.women"                
## [17] "GR2012.Hispanic.total"                                 
## [18] "GR2012.Hispanic.men"                                   
## [19] "GR2012.Hispanic.women"                                 
## [20] "GR2012.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "GR2012.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "GR2012.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "GR2012.White.total"                                    
## [24] "GR2012.White.men"                                      
## [25] "GR2012.White.women"                                    
## [26] "GR2012.Two.or.more.races.total"                        
## [27] "GR2012.Two.or.more.races.men"                          
## [28] "GR2012.Two.or.more.races.women"                        
## [29] "GR2012.Race.ethnicity.unknown.total"                   
## [30] "GR2012.Race.ethnicity.unknown.men"                     
## [31] "GR2012.Race.ethnicity.unknown.women"                   
## [32] "GR2012.Nonresident.alien.total"                        
## [33] "GR2012.Nonresident.alien.men"                          
## [34] "GR2012.Nonresident.alien.women"                        
## [35] "IDX_GR"
```

```r
# str(df5_1)

df5_2 <- read.csv("2012/raw/05_Graduation_rates_2.csv")
dim(df5_2)
```

```
## [1] 380  79
```

```r
names(df5_2)
```

```
##  [1] "unitid"                                                                                                     
##  [2] "institution.name"                                                                                           
##  [3] "year"                                                                                                       
##  [4] "GR200_12.Revised.bachelor.s.degree.seeking.cohort...cohort.year.2004."                                      
##  [5] "GR200_12.Exclusions.from.bachelor.s.degree.seeking.cohort.within.150..percent.of.normal.time"               
##  [6] "GR200_12.Adjusted.bachelor.s.degree.seeking.cohort.within.150..of.normal.time"                              
##  [7] "GR200_12.Number.completed.a.bachelor.s.degree.within.100..of.normal.time..4.years."                         
##  [8] "GR200_12.Graduation.rate...bachelor.s.degree.within.100..of.normal.time..4.years."                          
##  [9] "GR200_12.Number.completed.a.bachelor.s.degree.within.150..of.normal.time..6.years."                         
## [10] "GR200_12.Graduation.rate...bachelor.s.degree.within.150..of.normal.time..6.years."                          
## [11] "GR200_12.Additional.exclusions.from.bachelor.s.degree.seeking.cohort"                                       
## [12] "GR200_12.Adjusted.bachelor.s.degree.seeking.cohort.within.200..of.normal.time"                              
## [13] "GR200_12.Number.completed.a.bachelor.s.degree.between.150..and.200..of.normal.time"                         
## [14] "GR200_12.Number.completed.a.bachelor.s.degree.within.200..of.normal.time..8.years."                         
## [15] "GR200_12.Graduation.rate...bachelor.s.degree.within.200..of.normal.time..8.years."                          
## [16] "GR200_12.Still.enrolled"                                                                                    
## [17] "GR200_12.Revised.degree.certificate.seeking.cohort...cohort.year.2008."                                     
## [18] "GR200_12.Exclusions.from.degree.certificate.seeking.cohort.within.150..percent.of.normal.time"              
## [19] "GR200_12.Adjusted.degree.certificate.seeking.cohort.within.150..of.normal.time"                             
## [20] "GR200_12.Number.completed.a.degree.certificate.within.100..of.normal.time"                                  
## [21] "GR200_12.Graduation.rate...degree.certificate.within.100..of.normal.time"                                   
## [22] "GR200_12.Number.completed.a.degree.certificate..within.150..of.normal.time"                                 
## [23] "GR200_12.Graduation.rate...degree.certificate.within.150..of.normal.time"                                   
## [24] "GR200_12.Additional.exclusions.from.degree.certificate.seeking.cohort"                                      
## [25] "GR200_12.Adjusted.degree.certificate.seeking.cohort.within.200..of.normal.time"                             
## [26] "GR200_12.Number.completed.a..degree.certificate.between.150..and.200..of.normal.time"                       
## [27] "GR200_12.Number.completed.a.degree.certificate.within.200..of.normal.time"                                  
## [28] "GR200_12.Graduation.rate...degree.certificate.within.200..of.normal.time"                                   
## [29] "GR200_12.Still.enrolled.1"                                                                                  
## [30] "FLAGS2012.Response.status...Graduation.Rates"                                                               
## [31] "FLAGS2012.Status.of.Graduation.rate.survey.when.data.collection.closed"                                     
## [32] "FLAGS2012.Parent.child.indicator...Graduation.Rates"                                                        
## [33] "FLAGS2012.UNITID.of.parent.institution.reporting.Graduation.Rates"                                          
## [34] "FLAGS2012.Imputation.method...Graduation.Rates"                                                             
## [35] "FLAGS2012.Enrolled.any.full.time.first.time.students"                                                       
## [36] "FLAGS2012.Parent.child.allocation.factor...Graduation.Rates"                                                
## [37] "FLAGS2012.Does.institution.use.a.website.to.disclose.Student.Right.to.Know.student.athlete.graduation.rates"
## [38] "FLAGS2012.Student.Right.to.Know.student.athlete.graduation.rate.website.URL"                                
## [39] "FLAGS2012.Response.status...Graduation.Rates.200"                                                           
## [40] "FLAGS2012.Status.of.Graduation.rate.200.survey.when.data.collection.closed"                                 
## [41] "FLAGS2012.Parent.child.indicator...Graduation.Rates.200"                                                    
## [42] "FLAGS2012.UNITID.of.parent.institution.reporting.Graduation.Rates.200"                                      
## [43] "FLAGS2012.Imputation.method...Graduation.Rates.200"                                                         
## [44] "GR2012_L2.Adjusted.cohort..revised.cohort.minus.exclusions."                                                
## [45] "GR2012_L2.Completers.within.100..of.normal.time"                                                            
## [46] "GR2012_L2.Completers.within.150..of.normal.time"                                                            
## [47] "GR2012_L2.Transfer.out.students"                                                                            
## [48] "GR2012_L2.Still.enrolled"                                                                                   
## [49] "GR2012_L2.No.longer.enrolled"                                                                               
## [50] "DRVGR2012.Graduation.rate..total.cohort"                                                                    
## [51] "DRVGR2012.Graduation.rate..men"                                                                             
## [52] "DRVGR2012.Graduation.rate..women"                                                                           
## [53] "DRVGR2012.Graduation.rate..American.Indian.or.Alaska.Native"                                                
## [54] "DRVGR2012.Graduation.rate..Asian.Native.Hawaiian.Other.Pacific.Islander"                                    
## [55] "DRVGR2012.Graduation.rate..Asian"                                                                           
## [56] "DRVGR2012.Graduation.rate..Native.Hawaiian.or.Other.Pacific.Islander"                                       
## [57] "DRVGR2012.Graduation.rate..Black..non.Hispanic"                                                             
## [58] "DRVGR2012.Graduation.rate..Hispanic"                                                                        
## [59] "DRVGR2012.Graduation.rate..White..non.Hispanic"                                                             
## [60] "DRVGR2012.Graduation.rate..two.or.more.races"                                                               
## [61] "DRVGR2012.Graduation.rate..Race.ethnicity.unknown"                                                          
## [62] "DRVGR2012.Graduation.rate..Nonresident.alien"                                                               
## [63] "DRVGR2012.Transfer.out.rate..total.cohort"                                                                  
## [64] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.4.years..total"                                        
## [65] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.5.years..total"                                        
## [66] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..total"                                        
## [67] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..men"                                          
## [68] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..women"                                        
## [69] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..American.Indian.or.Alaska.Native"             
## [70] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Asian.Native.Hawaiian.Pacific.Islander"       
## [71] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Asian"                                        
## [72] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Native.Hawaiian.or.Other.Pacific.Islander"    
## [73] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Black..non.Hispanic"                          
## [74] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Hispanic"                                     
## [75] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..White..non.Hispanic"                          
## [76] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..two.or.more.races"                            
## [77] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Race.ethnicity.unknown"                       
## [78] "DRVGR2012.Graduation.rate...bachelor.s.degree.within.6.years..Nonresident.alien"                            
## [79] "DRVGR2012.Transfer.out.rate...bachelor.s.cohort"
```

```r
# str(df5_2)
```



Category 6: Student financial aid and net price
-----------------------------------------------


```r
df6 <- read.csv("2012/raw/06_Student_financial_aid_and_net_price.csv")
dim(df6)
```

```
## [1] 380 295
```

```r
names(df6)
```

```
##   [1] "unitid"                                                                                                                                                     
##   [2] "institution.name"                                                                                                                                           
##   [3] "year"                                                                                                                                                       
##   [4] "FLAGS2012.Parent.child.allocation.factor...Student.Financial.Aid"                                                                                           
##   [5] "FLAGS2012.Response.status.for.Student.Financial.Aid.survey"                                                                                                 
##   [6] "FLAGS2012.Status.of.Student.Financial.Aid.Survey.when.data.collection.closed"                                                                               
##   [7] "FLAGS2012.Parent.child.indicator.Student.Financial.Aid.survey"                                                                                              
##   [8] "FLAGS2012.ID.number.of.parent.institution.Student.Financial.Aid"                                                                                            
##   [9] "FLAGS2012.Type.of.imputation.method.Student.Financial.Aid"                                                                                                  
##  [10] "SFA1112.Number.of.students.in.fall.cohort"                                                                                                                  
##  [11] "SFA1112.Students.in.fall.cohort.as.a.percentage.of.all.undergraduates"                                                                                      
##  [12] "SFA1112.Number.of.students.in.fall.cohort.who.are.paying.in.district.tuition.rates"                                                                         
##  [13] "SFA1112.Percentage.of.students.in.fall.cohort.who.are.paying.in.district.tuition.rates"                                                                     
##  [14] "SFA1112.Number.of.students.in.fall.cohort.who.are.paying.in.state.tuititon.rates"                                                                           
##  [15] "SFA1112.Percentage.of.students.in.fall.cohort.who.paying.in.state.tuition.rates"                                                                            
##  [16] "SFA1112.Number.of.students.in.fall.cohort.who.are.paying.out.of.state.tuition.rates"                                                                        
##  [17] "SFA1112.Percentage.of.students.in.fall.cohort.who.are.paying.out.of.state.tuition.rates"                                                                    
##  [18] "SFA1112.Number.of.students.in.fall.cohort.whose.residence.tuition.rate.is.unknown"                                                                          
##  [19] "SFA1112.Percentage.of.students.in.fall.cohort.whose.residence..tuition.rate.is.unknown"                                                                     
##  [20] "SFA1112.Total.number.of.undergraduates...fall.cohort"                                                                                                       
##  [21] "SFA1112.Number.of.students.in.full.year.cohort"                                                                                                             
##  [22] "SFA1112.Students.in.full.year.cohort.as.a.percentage.of.all..undergraduates"                                                                                
##  [23] "SFA1112.Number.of.students.in.full.year.cohort.who.are.paying.in.district.tuition.rates"                                                                    
##  [24] "SFA1112.Percentage.of.students.in.full.year.cohort.who.are.paying.in.district.tuition.rates"                                                                
##  [25] "SFA1112.Number.of.students.in.full.year.cohort.who.are.paying.in.state.tuition.rates"                                                                       
##  [26] "SFA1112.Percentage.of.students.in.full.year.cohort.who.are.paying.in.state.tuition.rates"                                                                   
##  [27] "SFA1112.Number.of.students.in.full.year.cohort.who.are.paying.out.of.state.tuition.rates"                                                                   
##  [28] "SFA1112.Percentage.of.students.in.full.year.cohort.who.are.paying.out.of.state.tuition.rates"                                                               
##  [29] "SFA1112.Number.of.students.in.full.year.cohort.whose.residence.tuition.rate.is.unknown"                                                                     
##  [30] "SFA1112.Percentage.of.students.in.full.year.cohort.whose.residence.tuition.rate..is.unknown"                                                                
##  [31] "SFA1112.Total.number.of.undergraduates...full.year.cohort"                                                                                                  
##  [32] "SFA1112.Total.number.of.full.time.first.time.degree.certificate.seeking.undergraduates...financial.aid.cohort"                                              
##  [33] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.any.financial.aid"                                                                          
##  [34] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.any.financial.aid"                                                                         
##  [35] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.any.loans.to.students.or.grant.aid..from.federal.state.local.government.or.the.institution" 
##  [36] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.any.loans.to.students.or.grant.aid..from.federal.state.local.government.or.the.institution"
##  [37] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.federal..state..local.or.institutional.grant.aid"                                           
##  [38] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.federal..state..local.or.institutional.grant.aid"                                          
##  [39] "SFA1112.Total.amount.of.federal..state..local.or.institutional.grant.aid.received.by.full.time.first.time.undergraduates"                                   
##  [40] "SFA1112.Average.amount.of.federal..state..local.or.institutional.grant.aid.received"                                                                        
##  [41] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.federal.grant.aid"                                                                          
##  [42] "SFA1112.Percent.of.full.time.first.time.undergraduates..receiving.federal.grant.aid"                                                                        
##  [43] "SFA1112.Total.amount.of.Federal.grant.aid.received.by.full.time.first.time.undergraduates"                                                                  
##  [44] "SFA1112.Average.amount.of.federal.grant.aid.received.by.full.time.first.time.undergraduates"                                                                
##  [45] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.Pell.grants"                                                                                
##  [46] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.Pell.grants"                                                                               
##  [47] "SFA1112.Total.amount.of.Pell.grant.aid.received.by.full.time.first.time.undergraduates"                                                                     
##  [48] "SFA1112.Average.amount.of.Pell.grant.aid.received.by.full.time.first.time.undergraduates"                                                                   
##  [49] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.other.federal.grant.aid"                                                                    
##  [50] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.other.federal.grant.aid"                                                                   
##  [51] "SFA1112.Total.amount.of.other.federal.grant.aid.received.by.full.time.first.time.undergraduates"                                                            
##  [52] "SFA1112.Average.amount.of.other.federal.grant.aid.received.by.full.time.first.time.undergraduates"                                                          
##  [53] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.state.local.grant.aid"                                                                      
##  [54] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.state.local.grant.aid"                                                                     
##  [55] "SFA1112.Total.amount.of.state.local.grant.aid.received.by.full.time.first.time.undergraduates"                                                              
##  [56] "SFA1112.Average.amount.of.state.local.grant.aid.received.by.full.time.first.time.undergraduates"                                                            
##  [57] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving..institutional.grant.aid"                                                                   
##  [58] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.institutional.grant.aid"                                                                   
##  [59] "SFA1112.Total.amount.of.institutional.grant.aid.received.by.full.time.first.time.undergraduates"                                                            
##  [60] "SFA1112.Average.amount.of.institutional.grant.aid.received.by.full.time.first.time.undergraduates"                                                          
##  [61] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.student.loan.aid"                                                                           
##  [62] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.student.loan.aid"                                                                          
##  [63] "SFA1112.Total.amount.of.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                                   
##  [64] "SFA1112.Average.amount.of.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                                 
##  [65] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.federal.student.loans"                                                                      
##  [66] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.federal.student.loans"                                                                     
##  [67] "SFA1112.Total.amount.of.Federal.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                           
##  [68] "SFA1112.Average.amount.of.federal.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                         
##  [69] "SFA1112.Number.of.full.time.first.time.undergraduates.receiving.other.student.loans"                                                                        
##  [70] "SFA1112.Percent.of.full.time.first.time.undergraduates.receiving.other.loan.aid"                                                                            
##  [71] "SFA1112.Total.amount.of.other.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                             
##  [72] "SFA1112.Average.amount.of.other.student.loan.aid.received.by.full.time.first.time.undergraduates"                                                           
##  [73] "SFA1112.Total.number.of.undergraduates...financial.aid.cohort"                                                                                              
##  [74] "SFA1112.Number.of.undergraduate.students.receiving.federal..state..local..institutional.or.other.sources.of.grant.aid"                                      
##  [75] "SFA1112.Percent.of.undergraduate.students.receiving.federal..state..local..institutional.or.other.sources.of.grant.aid"                                     
##  [76] "SFA1112.Total.amount.of.federal..state..local..institutional.or.other.sources.of.grant.aid.dollars.received.by.undergraduate.students"                      
##  [77] "SFA1112.Average.amount.of.federal..state..local..institutional.or.other.sources.of.grant.aid.dollars.received.by.undergraduate.students"                    
##  [78] "SFA1112.Number.of.undergraduate.students.receiving.Pell.grants"                                                                                             
##  [79] "SFA1112.Percent.of.undergraduate.students.receiving.Pell.grants"                                                                                            
##  [80] "SFA1112.Total.amount.of.Pell.grant.aid.received.by.undergraduate.students"                                                                                  
##  [81] "SFA1112.Average.amount.Pell.grant.aid.received.by.undergraduate.students"                                                                                   
##  [82] "SFA1112.Number.of.undergraduate.students.receiving.Federal.student.loans"                                                                                   
##  [83] "SFA1112.Percent.of.undergraduate.students.receiving.Federal.student.loans"                                                                                  
##  [84] "SFA1112.Total.amount.of.Federal.student.loan.aid.received.by.undergraduate.students"                                                                        
##  [85] "SFA1112.Average.amount.of.Federal.student.loan.aid.received.by.undergraduate.students"                                                                      
##  [86] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2011.12"                                                                             
##  [87] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2010.11"                                                                             
##  [88] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2009.10"                                                                             
##  [89] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid.2011.12"                                                      
##  [90] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                                
##  [91] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                                
##  [92] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                               
##  [93] "SFA1112.Average.net.price..income.over.110.000...students.receiving.Title.IV.Federal.financial.aid..2011.12"                                                
##  [94] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                                     
##  [95] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                                     
##  [96] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                                
##  [97] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                                
##  [98] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                                
##  [99] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                                
## [100] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                               
## [101] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                               
## [102] "SFA1112.Average.net.price..income.over.110.000...students.receiving.Title.IV.Federal.financial.aid..2009.10"                                                
## [103] "SFA1112.Average.net.price..income.over.110.000...students.receiving.Title.IV.Federal.financial.aid..2010.11"                                                
## [104] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2011.12.1"                                                                           
## [105] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2010.11.1"                                                                           
## [106] "SFA1112.Average.net.price.students.receiving.grant.or.scholarship.aid..2009.10.1"                                                                           
## [107] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                                     
## [108] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2011.12.1"                                              
## [109] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2011.12.1"                                              
## [110] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid.2011.12"                                                
## [111] "SFA1112.Average.net.price..income.over.110.000..students.receiving.Title.IV.Federal.financial.aid..2011.12"                                                 
## [112] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                                   
## [113] "SFA1112.Average.net.price..income.0.30.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                                   
## [114] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                              
## [115] "SFA1112.Average.net.price..income.30.001.48.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                              
## [116] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                              
## [117] "SFA1112.Average.net.price..income.48.001.75.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                              
## [118] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2009.10.1"                                             
## [119] "SFA1112.Average.net.price..income.75.001.110.000..students.receiving.Title.IV.Federal.financial.aid..2010.11.1"                                             
## [120] "SFA1112.Average.net.price..income.over.110.000..students.receiving.Title.IV.Federal.financial.aid..2009.10"                                                 
## [121] "SFA1112.Average.net.price..income.over.110.000..students.receiving.Title.IV.Federal.financial.aid..2010.11"                                                 
## [122] "SFA1112.Total.number..2011.12"                                                                                                                              
## [123] "SFA1112.Number.living.on.campus..2011.12"                                                                                                                   
## [124] "SFA1112.Number.living.off.campus.with.family..2011.12"                                                                                                      
## [125] "SFA1112.Number.living.off.campus.not.with.family..2011.12"                                                                                                  
## [126] "SFA1112.Number.living.arrangement.unknown..2011.12"                                                                                                         
## [127] "SFA1112.Total.amount.of.grant.and.scholarship.aid.received..2011.12"                                                                                        
## [128] "SFA1112.Average.amount.of.grant.and.scholarship.aid.received..2011.12"                                                                                      
## [129] "SFA1112.Total.number..2010.11"                                                                                                                              
## [130] "SFA1112.Number.living.on.campus..2010.11"                                                                                                                   
## [131] "SFA1112.Number.living.off.campus.with.family..2010.11"                                                                                                      
## [132] "SFA1112.Number.living.off.campus.not.with.family..2010.11"                                                                                                  
## [133] "SFA1112.Number.living.arrangement.unknown..2010.11"                                                                                                         
## [134] "SFA1112.Total.amount.of.grant.and.scholarship.aid.received..2010.11"                                                                                        
## [135] "SFA1112.Average.amount.of.grant.and.scholarship.aid.received..2010.11"                                                                                      
## [136] "SFA1112.Total.number..2009.10"                                                                                                                              
## [137] "SFA1112.Number.living.on.campus..2009.10"                                                                                                                   
## [138] "SFA1112.Number.living.off.campus.with.family..2009.10"                                                                                                      
## [139] "SFA1112.Number.living.off.campus.not.with.family..2009.10"                                                                                                  
## [140] "SFA1112.Number.living.arrangement.unknown..2009.10"                                                                                                         
## [141] "SFA1112.Total.amount.of.grant.and.scholarship.aid.received..2009.10"                                                                                        
## [142] "SFA1112.Average.amount.of.grant.and.scholarship.aid.received..2009.10"                                                                                      
## [143] "SFA1112.Total.number.in.all.income.levels..2011.12"                                                                                                         
## [144] "SFA1112.Number.living.on.campus.in.all.income.levels..2011.12"                                                                                              
## [145] "SFA1112.Number.living.off.campus.with.family.in.all.income.levels..2011.12"                                                                                 
## [146] "SFA1112.Number.living.off.campus.not.with.family.in.all.income.levels..2011.12"                                                                             
## [147] "SFA1112.Number.living.arrangement.unknown.in.all.income.levels..2011.12"                                                                                    
## [148] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.all.income.levels..2011.12"                                                                            
## [149] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.all.income.levels..2011.12"                                                                          
## [150] "SFA1112.Number.in.income.level..0.30.000...2011.12"                                                                                                         
## [151] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2011.12"                                                                      
## [152] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2011.12"                                                                    
## [153] "SFA1112.Number.in.income.level..30.001.48.000...2011.12"                                                                                                    
## [154] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000..2011.12"                                                                  
## [155] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2011.12"                                                               
## [156] "SFA1112.Number.in.income.level..48.001.75.000...2011.12"                                                                                                    
## [157] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2011.12"                                                                 
## [158] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2011.12"                                                               
## [159] "SFA1112.Number.in.income.level..75.001.110.000...2011.12"                                                                                                   
## [160] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2011.12"                                                                
## [161] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2011.12"                                                              
## [162] "SFA1112.Number.in.income.level..110.001.or.more...2011.12"                                                                                                  
## [163] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2011.12"                                                               
## [164] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2011.12"                                                             
## [165] "SFA1112.Total.number.in.all.income.levels..2010.11"                                                                                                         
## [166] "SFA1112.Number.living.on.campus.in.all.income.levels..2010.11"                                                                                              
## [167] "SFA1112.Number.living.off.campus.with.family.in.all.income.levels..2010.11"                                                                                 
## [168] "SFA1112.Number.living.off.campus.not.with.family.in.all.income.levels..2010.11"                                                                             
## [169] "SFA1112.Number.living.arrangement.unknown.in.all.income.levels..2010.11"                                                                                    
## [170] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.all.income.levels..2010.11"                                                                            
## [171] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.all.income.levels..2010.11"                                                                          
## [172] "SFA1112.Number.in.income.level..0.30.000...2010.11"                                                                                                         
## [173] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2010.11"                                                                      
## [174] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2010.11"                                                                    
## [175] "SFA1112.Number.in.income.level..30.001.48.000...2010.11"                                                                                                    
## [176] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2010.11"                                                                 
## [177] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2010.11"                                                               
## [178] "SFA1112.Number.in.income.level..48.001.75.000...2010.11"                                                                                                    
## [179] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2010.11"                                                                 
## [180] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2010.11"                                                               
## [181] "SFA1112.Number.in.income.level..75.001.110.000...2010.11"                                                                                                   
## [182] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2010.11"                                                                
## [183] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2010.11"                                                              
## [184] "SFA1112.Number.in.income.level..110.001.or.more...2010.11"                                                                                                  
## [185] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2010.11"                                                               
## [186] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2010.11"                                                             
## [187] "SFA1112.Total.number.in.all.income.levels..2009.10"                                                                                                         
## [188] "SFA1112.Number.living.on.campus.in.all.income.levels..2009.10"                                                                                              
## [189] "SFA1112.Number.living.off.campus.with.family.in.all.income.levels..2009.10"                                                                                 
## [190] "SFA1112.Number.living.off.campus.not.with.family.in.all.income.levels..2009.10"                                                                             
## [191] "SFA1112.Number.living.arrangement.unknown.in.all.income.levels..2009.10"                                                                                    
## [192] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.all.income.levels..2009.10"                                                                            
## [193] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.all.income.levels..2009.10"                                                                          
## [194] "SFA1112.Number.in.income.level..0.30.000...2009.10"                                                                                                         
## [195] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2009.10"                                                                      
## [196] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2009.10"                                                                    
## [197] "SFA1112.Number.in.income.level..30.001.48.000...2009.10"                                                                                                    
## [198] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2009.10"                                                                 
## [199] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2009.10"                                                               
## [200] "SFA1112.Number.in.income.level..48.001.75.000...2009.10"                                                                                                    
## [201] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2009.10"                                                                 
## [202] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2009.10"                                                               
## [203] "SFA1112.Number.in.income.level..75.001.110.000...2009.10"                                                                                                   
## [204] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2009.10"                                                                
## [205] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2009.10"                                                              
## [206] "SFA1112.Number.in.income.level..110.001.or.more...2009.10"                                                                                                  
## [207] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2009.10"                                                               
## [208] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2009.10"                                                             
## [209] "SFA1112.Total.number..2011.12.1"                                                                                                                            
## [210] "SFA1112.Number.living.on.campus..2011.12.1"                                                                                                                 
## [211] "SFA1112.Number.living.off.campus.with.family..2011.12.1"                                                                                                    
## [212] "SFA1112.Number.living.off.campus.not.with.family..2011.12.1"                                                                                                
## [213] "SFA1112.Number.living.arrangement.unknown..2011.12.1"                                                                                                       
## [214] "SFA1112.Total.amount.of.grant.and.scholarship.aid.received..2011.12.1"                                                                                      
## [215] "SFA1112.Average.amount.of.grant.and.scholarship.aid.received..2011.12.1"                                                                                    
## [216] "SFA1112.Total.number..2010.11.1"                                                                                                                            
## [217] "SFA1112.Number.living.on.campus..2010.11.1"                                                                                                                 
## [218] "SFA1112.Number.living.off.campus.with.family..2010.11.1"                                                                                                    
## [219] "SFA1112.Number.living.off.campus.not.with.family..2010.11.1"                                                                                                
## [220] "SFA1112.Number.living.arrangement.unknown..2010.11.1"                                                                                                       
## [221] "SFA1112.Total.amount.of.grant.and.scholarship.aid.received..2010.11.1"                                                                                      
## [222] "SFA1112.Average.amount.of.grant.and.scholarship.aid.received..2010.11.1"                                                                                    
## [223] "SFA1112.Total.number..2009.10.1"                                                                                                                            
## [224] "SFA1112.Number.living.on.campus..2009.10.1"                                                                                                                 
## [225] "SFA1112.Number.living.off.campus.with.family..2009.10.1"                                                                                                    
## [226] "SFA1112.Number.living.off.campus.not.with.family..2009.10.1"                                                                                                
## [227] "SFA1112.Number.living.arrangement.unknown..2009.10.1"                                                                                                       
## [228] "SFA1112.Total.amount.of.grant.and.scholarship.aid.received..2009.10.1"                                                                                      
## [229] "SFA1112.Average.amount.of.grant.and.scholarship.aid.received..2009.10.1"                                                                                    
## [230] "SFA1112.Total.number.in.all.income.levels..2011.12.1"                                                                                                       
## [231] "SFA1112.Number.living.on.campus.in.all.income.levels..2011.12.1"                                                                                            
## [232] "SFA1112.Number.living.off.campus.with.family.in.all.income.levels..2011.12.1"                                                                               
## [233] "SFA1112.Number.living.off.campus.not.with.family.in.all.income.levels..2011.12.1"                                                                           
## [234] "SFA1112.Number.living.arrangement.unknown.in.all.income.levels..2011.12.1"                                                                                  
## [235] "SFA1112.Total.amount.of.grant.and.scholarship.aid.all.income.levels..2011.12"                                                                               
## [236] "SFA1112.Average.amount.of.grant.and.scholarship.aid.all.income.levels..2011.12"                                                                             
## [237] "SFA1112.Number.in.income.level..0.30.000...2011.12.1"                                                                                                       
## [238] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2011.12.1"                                                                    
## [239] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2011.12.1"                                                                  
## [240] "SFA1112.Number.in.income.level..30.001.48.000...2011.12.1"                                                                                                  
## [241] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2011.12"                                                                 
## [242] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2011.12.1"                                                             
## [243] "SFA1112.Number.in.income.level..48.001.75.000...2011.12.1"                                                                                                  
## [244] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2011.12.1"                                                               
## [245] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2011.12.1"                                                             
## [246] "SFA1112.Number.in.income.level..75.001.110.000...2011.12.1"                                                                                                 
## [247] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2011.12.1"                                                              
## [248] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000..2011.12"                                                               
## [249] "SFA1112.Number.in.income.level..110.001.or.more...2011.12.1"                                                                                                
## [250] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2011.12.1"                                                             
## [251] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2011.12.1"                                                           
## [252] "SFA1112.Total.number.in.all.income.levels..2010.11.1"                                                                                                       
## [253] "SFA1112.Number.living.on.campus.in.all.income.levels..2010.11.1"                                                                                            
## [254] "SFA1112.Number.living.off.campus.with.family.in.all.income.levels..2010.11.1"                                                                               
## [255] "SFA1112.Number.living.off.campus.not.with.family.in.all.income.levels..2010.11.1"                                                                           
## [256] "SFA1112.Number.living.arrangement.unknown.in.all.income.levels..2010.11.1"                                                                                  
## [257] "SFA1112.Total.amount.of.grant.and.scholarship.aid.all.income.levels..2010.11"                                                                               
## [258] "SFA1112.Average.amount.of.grant.and.scholarship.aid.all.income.levels..2010.11"                                                                             
## [259] "SFA1112.Number.in.income.level..0.30.000...2010.11.1"                                                                                                       
## [260] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2010.11.1"                                                                    
## [261] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2010.11.1"                                                                  
## [262] "SFA1112.Number.in.income.level..30.001.48.000...2010.11.1"                                                                                                  
## [263] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2010.11.1"                                                               
## [264] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2010.11.1"                                                             
## [265] "SFA1112.Number.in.income.level..48.001.75.000...2010.11.1"                                                                                                  
## [266] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2010.11.1"                                                               
## [267] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2010.11.1"                                                             
## [268] "SFA1112.Number.in.income.level..75.001.110.000...2010.11.1"                                                                                                 
## [269] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2010.11.1"                                                              
## [270] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2010.11.1"                                                            
## [271] "SFA1112.Number.in.income.level..110.001.or.more...2010.11.1"                                                                                                
## [272] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2010.11.1"                                                             
## [273] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2010.11.1"                                                           
## [274] "SFA1112.Total.number.in.all.income.levels..2009.10.1"                                                                                                       
## [275] "SFA1112.Number.living.on.campus.in.all.income.levels..2009.10.1"                                                                                            
## [276] "SFA1112.Number.living.off.campus.with.family.in.all.income.levels..2009.10.1"                                                                               
## [277] "SFA1112.Number.living.off.campus.not.with.family.in.all.income.levels..2009.10.1"                                                                           
## [278] "SFA1112.Number.living.arrangement.unknown.in.all.income.levels..2009.10.1"                                                                                  
## [279] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.all.income.levels..2009.10.1"                                                                          
## [280] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.all.income.levels..2009.10.1"                                                                        
## [281] "SFA1112.Number.in.income.level..0.30.000...2009.10.1"                                                                                                       
## [282] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2009.10.1"                                                                    
## [283] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..0.30.000...2009.10.1"                                                                  
## [284] "SFA1112.Number.in.income.level..30.001.48.000...2009.10.1"                                                                                                  
## [285] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2009.10.1"                                                               
## [286] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..30.001.48.000...2009.10.1"                                                             
## [287] "SFA1112.Number.in.income.level..48.001.75.000...2009.10.1"                                                                                                  
## [288] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2009.10.1"                                                               
## [289] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..48.001.75.000...2009.10.1"                                                             
## [290] "SFA1112.Number.in.income.level..75.001.110.000...2009.10.1"                                                                                                 
## [291] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2009.10.1"                                                              
## [292] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..75.001.110.000...2009.10.1"                                                            
## [293] "SFA1112.Number.in.income.level..110.001.or.more...2009.10.1"                                                                                                
## [294] "SFA1112.Total.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2009.10.1"                                                             
## [295] "SFA1112.Average.amount.of.grant.and.scholarship.aid.in.income.level..110.001.or.more...2009.10.1"
```

```r
# str(df6)
```



Category 7: Student financial aid and net price
-----------------------------------------------


```r
df7 <- read.csv("2012/raw/07_Finance.csv")
dim(df7)
```

```
## [1] 380 507
```

```r
names(df7)
```

```
##   [1] "unitid"                                                                                                                                                 
##   [2] "institution.name"                                                                                                                                       
##   [3] "year"                                                                                                                                                   
##   [4] "FLAGS2012.Response.status.for.Finance.survey"                                                                                                           
##   [5] "FLAGS2012.Status.of.Finance.survey.when.data.collection.closed"                                                                                         
##   [6] "FLAGS2012.Parent.child.indicator.for.Finance.survey"                                                                                                    
##   [7] "FLAGS2012.ID.number.of.parent.institution.for.Finance.survey"                                                                                           
##   [8] "FLAGS2012.Parent.child.allocation.factor...Finance"                                                                                                     
##   [9] "FLAGS2012.Type.of.imputation.method..Finance"                                                                                                           
##  [10] "FLAGS2012.Identifies.reporting.standards.GASB..FASB..or.modified.FASB.for.profit.institutions..used.to.report.finance.data"                             
##  [11] "FLAGS2012.Beginning.date.of.fiscal.year.covered..all.finance."                                                                                          
##  [12] "FLAGS2012.End.date.of.fiscal.year.covered...all.finance."                                                                                               
##  [13] "FLAGS2012.Clean.Opinion.GPFS.from.auditor..all.finance."                                                                                                
##  [14] "FLAGS2012.GASB.alternative.accounting.model"                                                                                                            
##  [15] "FLAGS2012.Are.intercollegiate.athletic.expenses.accounted.for.as.auxiliary.enterprises.or.treated.as.student.services."                                 
##  [16] "FLAGS2012.Account.for.Pell.grants.as.pass.through.transactions.or.as.federal.grant.revenues.to.the.institution..FASB..institutions.."                   
##  [17] "FLAGS2012.Account.for.Pell.grants.as.pass.through.transactions.or.as.federal.grant.revenues.to.the.institution..private.for.profit.institutions.."      
##  [18] "F1112_F2.Long.term.investments"                                                                                                                         
##  [19] "F1112_F2.Total.assets"                                                                                                                                  
##  [20] "F1112_F2.Total.liabilities"                                                                                                                             
##  [21] "F1112_F2.Debt.related.to.Property..Plant..and.Equipment"                                                                                                
##  [22] "F1112_F2.Total.unrestricted.net.assets"                                                                                                                 
##  [23] "F1112_F2.Total.restricted.net.assets"                                                                                                                   
##  [24] "F1112_F2.Permanently.restricted.net.assets.included.in.total.restricted.net.assets"                                                                     
##  [25] "F1112_F2.Temporarily.restricted.net.assets"                                                                                                             
##  [26] "F1112_F2.Total.net.assets"                                                                                                                              
##  [27] "F1112_F2.Land..improvements...End.of.year"                                                                                                              
##  [28] "F1112_F2.Buildings...End.of.year"                                                                                                                       
##  [29] "F1112_F2.Equipment..including.art.and.library.collections...End.of.year"                                                                                
##  [30] "F1112_F2.Construction.in.Progress"                                                                                                                      
##  [31] "F1112_F2.Other.plant..property.and.equipment"                                                                                                           
##  [32] "F1112_F2.Total.Plant..Property..and.Equipment"                                                                                                          
##  [33] "F1112_F2.Accumulated.depreciation"                                                                                                                      
##  [34] "F1112_F2.Property..Plant..and.Equipment..net.of.accumulated.depreciation"                                                                               
##  [35] "F1112_F2.Intangible.Assets..net.of.accumulated.amortization"                                                                                            
##  [36] "F1112_F2.Total.revenues.and.investment.return"                                                                                                          
##  [37] "F1112_F2.Total.expenses"                                                                                                                                
##  [38] "F1112_F2.Other.specific.changes.in.net.assets"                                                                                                          
##  [39] "F1112_F2.Total.change.in.net.assets"                                                                                                                    
##  [40] "F1112_F2.Net.assets..beginning.of.the.year"                                                                                                             
##  [41] "F1112_F2.Adjustments.to.beginning.of.year.net.assets"                                                                                                   
##  [42] "F1112_F2.Net.assets..end.of.the.year"                                                                                                                   
##  [43] "F1112_F2.Pell.grants"                                                                                                                                   
##  [44] "F1112_F2.Other.federal.grants"                                                                                                                          
##  [45] "F1112_F2.State.grants"                                                                                                                                  
##  [46] "F1112_F2.Local.grants"                                                                                                                                  
##  [47] "F1112_F2.Institutional.grants..funded."                                                                                                                 
##  [48] "F1112_F2.Institutional.grants..unfunded."                                                                                                               
##  [49] "F1112_F2.Total.student.grants"                                                                                                                          
##  [50] "F1112_F2.Allowances.applied.to.tuition.and.fees"                                                                                                        
##  [51] "F1112_F2.Allowances.applied.to.auxiliary.enterprise.revenues"                                                                                           
##  [52] "F1112_F2.Tuition.and.fees...Total"                                                                                                                      
##  [53] "F1112_F2.Tuition.and.fees...Unrestricted"                                                                                                               
##  [54] "F1112_F2.Tuition.and.fees...Temporarily.restricted"                                                                                                     
##  [55] "F1112_F2.Tuition.and.fees...Permanently.restricted"                                                                                                     
##  [56] "F1112_F2.Federal.appropriations...Total"                                                                                                                
##  [57] "F1112_F2.Federal.appropriations...Unrestricted"                                                                                                         
##  [58] "F1112_F2.Federal.appropriations...Temporarily.restricted"                                                                                               
##  [59] "F1112_F2.Federal.appropriations...Permanently.restricted"                                                                                               
##  [60] "F1112_F2.State.appropriations...Total"                                                                                                                  
##  [61] "F1112_F2.State.appropriations...Unrestricted"                                                                                                           
##  [62] "F1112_F2.State.appropriations...Temporarily.restricted"                                                                                                 
##  [63] "F1112_F2.State.appropriations...Permanently.restricted"                                                                                                 
##  [64] "F1112_F2.Local.appropriations...Total"                                                                                                                  
##  [65] "F1112_F2.Local.appropriations...Unrestricted"                                                                                                           
##  [66] "F1112_F2.Local.appropriations....Temporarily.restricted"                                                                                                
##  [67] "F1112_F2.Local.appropriations...Permanently.restricted"                                                                                                 
##  [68] "F1112_F2.Federal.grants.and.contracts...Total"                                                                                                          
##  [69] "F1112_F2.Federal.grants.and.contracts...Unrestricted"                                                                                                   
##  [70] "F1112_F2.Federal.grants.and.contracts....Temporarily.restricted"                                                                                        
##  [71] "F1112_F2.Federal.grants.and.contracts...Pemanently.restricted"                                                                                          
##  [72] "F1112_F2.State.grants.and.contracts...Total"                                                                                                            
##  [73] "F1112_F2.State.grants.and.contracts...Unrestricted"                                                                                                     
##  [74] "F1112_F2.State.grants.and.contracts...Temporarily.restricted"                                                                                           
##  [75] "F1112_F2.State.grants.and.contracts...Permanently.restricted"                                                                                           
##  [76] "F1112_F2.Local.grants.and.contracts...Total"                                                                                                            
##  [77] "F1112_F2.Local.grants.and.contracts...Unrestricted"                                                                                                     
##  [78] "F1112_F2.Local.grants.and.contracts...Temporarily.restricted"                                                                                           
##  [79] "F1112_F2.Local.grants.and.contracts....Permanently.restricted"                                                                                          
##  [80] "F1112_F2.Private.gifts..grants..and.contracts...Total"                                                                                                  
##  [81] "F1112_F2.Private.gifts..grants..and.contracts...Unrestricted"                                                                                           
##  [82] "F1112_F2.Private.gifts...Unrestricted"                                                                                                                  
##  [83] "F1112_F2.Private.grants.and.contracts...Unrestricted"                                                                                                   
##  [84] "F1112_F2.Private.gifts..grants.and.contracts...Temporarily.restricted"                                                                                  
##  [85] "F1112_F2.Private.gifts...Temporarily.restricted"                                                                                                        
##  [86] "F1112_F2.Private.grants.and.contracts...Temporarily.restricted"                                                                                         
##  [87] "F1112_F2.Private.gifts..grants..and.contracts...Permanently.restricted"                                                                                 
##  [88] "F1112_F2.Private.gifts...Permanentlly.restricted"                                                                                                       
##  [89] "F1112_F2.Private.grants..and.contracts...Permanently.restricted"                                                                                        
##  [90] "F1112_F2.Private.gifts...Total"                                                                                                                         
##  [91] "F1112_F2.Private.grants.and.contrants...Total"                                                                                                          
##  [92] "F1112_F2.Contributions.from.affiliated.entities...Total"                                                                                                
##  [93] "F1112_F2.Contributions.from.affiliated.entities...Unrestricted"                                                                                         
##  [94] "F1112_F2.Contributions.from.affiliated.entities...Temporarily.restricted"                                                                               
##  [95] "F1112_F2.Contributions.from.affiliated.entities...Permanently.restricted"                                                                               
##  [96] "F1112_F2.Investment.return...Total"                                                                                                                     
##  [97] "F1112_F2.Investment.return...Unrestricted"                                                                                                              
##  [98] "F1112_F2.Investment.return...Temporarily.restricted"                                                                                                    
##  [99] "F1112_F2.Investment.return...Permanently.restricted"                                                                                                    
## [100] "F1112_F2.Sales.and.services.of.educational.activities...Total"                                                                                          
## [101] "F1112_F2.Sales.and.services.of.educational.activities...Unrestricted"                                                                                   
## [102] "F1112_F2.Sales.and.services.of.auxiliary.enterprises...Total"                                                                                           
## [103] "F1112_F2.Sales.and.services.of.auxiliary.enterprises...Unrestricted"                                                                                    
## [104] "F1112_F2.Hospital.revenue...Total"                                                                                                                      
## [105] "F1112_F2.Hospital.revenue...Unrestricted"                                                                                                               
## [106] "F1112_F2.Independent.operations.revenue...Total"                                                                                                        
## [107] "F1112_F2.Independent.operations.revenue...Unrestricted"                                                                                                 
## [108] "F1112_F2.Independent.operations.revenue...Temporarily.restricted"                                                                                       
## [109] "F1112_F2.Independent.operations.revenue...Permanently.restricted"                                                                                       
## [110] "F1112_F2.Other.revenue...Total"                                                                                                                         
## [111] "F1112_F2.Other.revenue...Unrestricted"                                                                                                                  
## [112] "F1112_F2.Other.revenue...Temporarily.restricted"                                                                                                        
## [113] "F1112_F2.Other.revenue...Permanently.restricted"                                                                                                        
## [114] "F1112_F2.Total.revenues.and.investment.return...Total"                                                                                                  
## [115] "F1112_F2.Total.revenues.and.investment.return...Unrestricted"                                                                                           
## [116] "F1112_F2.Total.revenues.and.investment.return...Temporarily.restricted"                                                                                 
## [117] "F1112_F2.Total.revenues.and.investment.return...Permanently.restricted"                                                                                 
## [118] "F1112_F2.Net.assets.released.from.restriction...Total"                                                                                                  
## [119] "F1112_F2.Net.assets.released.from.restriction...Unrestricted"                                                                                           
## [120] "F1112_F2.Net.assets.released.from.restriction...Temporarily.restricted"                                                                                 
## [121] "F1112_F2.Net.assets.released.from.restriction...Permanently.restricted"                                                                                 
## [122] "F1112_F2.Net.total.revenues..after.assets.released.from.restriction...Total"                                                                            
## [123] "F1112_F2.Net.total.revenues..after.assets.released.from.restriction...Unrestricted"                                                                     
## [124] "F1112_F2.Net.total.revenues..after.assets.released.from.restriction...Temporarily.restricted"                                                           
## [125] "F1112_F2.Net.total.revenues..after.assets.released.from.restriction...Permanently.restricted"                                                           
## [126] "F1112_F2.Instruction.Total.amount"                                                                                                                      
## [127] "F1112_F2.Instruction.Salaries.and.wages"                                                                                                                
## [128] "F1112_F2.Instruction.Benefits"                                                                                                                          
## [129] "F1112_F2.Instruction.Operation.and.maintenance.of.plant"                                                                                                
## [130] "F1112_F2.Instruction.Depreciation"                                                                                                                      
## [131] "F1112_F2.Instruction.Interest"                                                                                                                          
## [132] "F1112_F2.Instruction.All.other"                                                                                                                         
## [133] "F1112_F2.Research.Total.amount"                                                                                                                         
## [134] "F1112_F2.Research.Salaries.and.wages"                                                                                                                   
## [135] "F1112_F2.Research.Benefits"                                                                                                                             
## [136] "F1112_F2.Research.Operation.and.maintenance.of.plant"                                                                                                   
## [137] "F1112_F2.Research.Depreciation"                                                                                                                         
## [138] "F1112_F2.Research.Interest"                                                                                                                             
## [139] "F1112_F2.Research.All.other"                                                                                                                            
## [140] "F1112_F2.Public.service.Total.amount"                                                                                                                   
## [141] "F1112_F2.Public.service.Salaries.and.wages"                                                                                                             
## [142] "F1112_F2.Public.service.Benefits"                                                                                                                       
## [143] "F1112_F2.Public.service.Operation.and.maintenance.of.plant"                                                                                             
## [144] "F1112_F2.Public.service.Depreciation"                                                                                                                   
## [145] "F1112_F2.Public.service.Interest"                                                                                                                       
## [146] "F1112_F2.Public.service.All.other"                                                                                                                      
## [147] "F1112_F2.Academic.support.Total.amount"                                                                                                                 
## [148] "F1112_F2.Academic.support.Salaries.and.wages"                                                                                                           
## [149] "F1112_F2.Academic.support.Benefits"                                                                                                                     
## [150] "F1112_F2.Academic.support.Operation.and.maintenance.of.plant"                                                                                           
## [151] "F1112_F2.Academic.support.Depreciation"                                                                                                                 
## [152] "F1112_F2.Academic.support.Interest"                                                                                                                     
## [153] "F1112_F2.Academic.support.All.other"                                                                                                                    
## [154] "F1112_F2.Student.service.Total.amount"                                                                                                                  
## [155] "F1112_F2.Student.service.Salaries.and.wages"                                                                                                            
## [156] "F1112_F2.Student.service.Benefits"                                                                                                                      
## [157] "F1112_F2.Student.service.Operation.and.maintenance.of.plant"                                                                                            
## [158] "F1112_F2.Student.service.Depreciation"                                                                                                                  
## [159] "F1112_F2.Student.service.Interest"                                                                                                                      
## [160] "F1112_F2.Student.service.All.other"                                                                                                                     
## [161] "F1112_F2.Institutional.support.Total.amount"                                                                                                            
## [162] "F1112_F2.Institutional.support.Salaries.and.wages"                                                                                                      
## [163] "F1112_F2.Institutional.support.Benefits"                                                                                                                
## [164] "F1112_F2.Institutional.support.Operation.and.maintenance.of.plant"                                                                                      
## [165] "F1112_F2.Institutional.support.Depreciation"                                                                                                            
## [166] "F1112_F2.Institutional.support.Interest"                                                                                                                
## [167] "F1112_F2.Institutional.support.All.other"                                                                                                               
## [168] "F1112_F2.Auxiliary.enterprises.Total.amount"                                                                                                            
## [169] "F1112_F2.Auxiliary.enterprises.Salaries.and.wages"                                                                                                      
## [170] "F1112_F2.Auxiliary.enterprises.Benefits"                                                                                                                
## [171] "F1112_F2.Auxiliary.enterprises.Operation.and.maintenance.of.plant"                                                                                      
## [172] "F1112_F2.Auxiliary.enterprises.Depreciation"                                                                                                            
## [173] "F1112_F2.Auxiliary.enterprises.Interest"                                                                                                                
## [174] "F1112_F2.Auxiliary.enterprises.All.other"                                                                                                               
## [175] "F1112_F2.Net.grant.aid.to.students.Total.amount"                                                                                                        
## [176] "F1112_F2.Net.grant.aid.to.students.All.other"                                                                                                           
## [177] "F1112_F2.Hospital.services.Total.amount"                                                                                                                
## [178] "F1112_F2.Hospital.services.Salaries.and.wages"                                                                                                          
## [179] "F1112_F2.Hospital.services.Benefits"                                                                                                                    
## [180] "F1112_F2.Hospital.services.Operation.and.maintenance.of.plant"                                                                                          
## [181] "F1112_F2.Hospital.services.Depreciation"                                                                                                                
## [182] "F1112_F2.Hospital.services.Interest"                                                                                                                    
## [183] "F1112_F2.Hospital.services.All.other"                                                                                                                   
## [184] "F1112_F2.Independent.operations.Total.Amount"                                                                                                           
## [185] "F1112_F2.Independent.operations.Salaries.and.wages"                                                                                                     
## [186] "F1112_F2.Independent.operations.Benefits"                                                                                                               
## [187] "F1112_F2.Independent.operations.Operation.and.maintenance.of.plant"                                                                                     
## [188] "F1112_F2.Independent.operations.Depreciation"                                                                                                           
## [189] "F1112_F2.Independent.operations.Interest"                                                                                                               
## [190] "F1112_F2.Independent.operations.All.other"                                                                                                              
## [191] "F1112_F2.Operation.and.maintenance.of.plant.Total.amount"                                                                                               
## [192] "F1112_F2.Operation.and.maintenance.of.plant.Salaries.and.wages"                                                                                         
## [193] "F1112_F2.Operation.and.maintenance.of.plant.Benefits"                                                                                                   
## [194] "F1112_F2.Operation.and.maintenance.of.plant.Operation.and.maintenance.of.plant"                                                                         
## [195] "F1112_F2.Operation.and.maintenance.of.plant.Depreciation"                                                                                               
## [196] "F1112_F2.Operation.and.maintenance.of.plant.Interest"                                                                                                   
## [197] "F1112_F2.Operation.and.maintenance.of.plant.All.other"                                                                                                  
## [198] "F1112_F2.Other.expenses.Total.amount"                                                                                                                   
## [199] "F1112_F2.Other.expenses.Salaries.and.wages"                                                                                                             
## [200] "F1112_F2.Other.expenses.Benefits"                                                                                                                       
## [201] "F1112_F2.Other.expenses.Operation.and.maintenance.of.plant"                                                                                             
## [202] "F1112_F2.Other.expenses.Depreciation"                                                                                                                   
## [203] "F1112_F2.Other.expenses.Interest"                                                                                                                       
## [204] "F1112_F2.Other.expenses.All.other"                                                                                                                      
## [205] "F1112_F2.Total.expenses.Total.amount"                                                                                                                   
## [206] "F1112_F2.Total.expenses.Salaries.and.wages"                                                                                                             
## [207] "F1112_F2.Total.expenses.Benefits"                                                                                                                       
## [208] "F1112_F2.Total.expenses.Operation.and.maintenance.of.plant"                                                                                             
## [209] "F1112_F2.Total.expenses.Depreciation"                                                                                                                   
## [210] "F1112_F2.Total.expenses.Interest"                                                                                                                       
## [211] "F1112_F2.Total.expenses.All.other"                                                                                                                      
## [212] "F1112_F2.Does.this.institution.or.any.of.its.foundations.or.other.affiliated.organizations.own.endowment.assets.."                                      
## [213] "F1112_F2.Value.of.endowment.assets.at.the.beginning.of.the.fiscal.year"                                                                                 
## [214] "F1112_F2.Value.of.endowment.assets.at.the.end.of.the.fiscal.year"                                                                                       
## [215] "F1112_F3.Total.assets"                                                                                                                                  
## [216] "F1112_F3.Total.liabilities"                                                                                                                             
## [217] "F1112_F3.Total.equity"                                                                                                                                  
## [218] "F1112_F3.Total.liabilities.and.equity"                                                                                                                  
## [219] "F1112_F3.Total.revenues.and.investment.return"                                                                                                          
## [220] "F1112_F3.Total.expenses"                                                                                                                                
## [221] "F1112_F3.Sum.of.specific.changes.in.equity"                                                                                                             
## [222] "F1112_F3.Net.income"                                                                                                                                    
## [223] "F1112_F3.Other.changes.in.equity"                                                                                                                       
## [224] "F1112_F3.Equity..beginning.of.year"                                                                                                                     
## [225] "F1112_F3.Adjustments.to.beginning.net.equity"                                                                                                           
## [226] "F1112_F3.Equity..end.of.year"                                                                                                                           
## [227] "F1112_F3.Pell.grants"                                                                                                                                   
## [228] "F1112_F3.Other.federal.grants"                                                                                                                          
## [229] "F1112_F3.State.and.local.grants"                                                                                                                        
## [230] "F1112_F3.Institutional.grants"                                                                                                                          
## [231] "F1112_F3.Total.student.grants"                                                                                                                          
## [232] "F1112_F3.Allowances.applied.to.tuition.and.fees"                                                                                                        
## [233] "F1112_F3.Allowances.applied.to.auxiliary.enterprise.revenues"                                                                                           
## [234] "F1112_F3.Tuition.and.fees"                                                                                                                              
## [235] "F1112_F3.Federal.appropriations..grants.and.contracts"                                                                                                  
## [236] "F1112_F3.State.and.local.appropriations..grants.and.contracts"                                                                                          
## [237] "F1112_F3.Private.grants.and.contracts"                                                                                                                  
## [238] "F1112_F3.Investment.income.and.investment.gains..losses..included.in.net.income"                                                                        
## [239] "F1112_F3.Sales.and.services.of.educational.activities"                                                                                                  
## [240] "F1112_F3.Sales.and.services.of.auxiliary.enterprises"                                                                                                   
## [241] "F1112_F3.Other.revenue"                                                                                                                                 
## [242] "F1112_F3.Total.revenues.and.investment.return.1"                                                                                                        
## [243] "F1112_F3.Instruction"                                                                                                                                   
## [244] "F1112_F3.Research.and.public.service"                                                                                                                   
## [245] "F1112_F3.Academic.and..institutional.support..and..student.services"                                                                                    
## [246] "F1112_F3.Auxiliary.enterprises"                                                                                                                         
## [247] "F1112_F3.Net.grant.aid.to.students"                                                                                                                     
## [248] "F1112_F3.All.other.expenses"                                                                                                                            
## [249] "F1112_F3.Total.expenses.1"                                                                                                                              
## [250] "F1112_F1A.Total.current.assets"                                                                                                                         
## [251] "F1112_F1A.Depreciable.capital.assets..net.of.depreciation"                                                                                              
## [252] "F1112_F1A.Other.noncurrent.assets"                                                                                                                      
## [253] "F1112_F1A.Total.noncurrent.assets"                                                                                                                      
## [254] "F1112_F1A.Total.assets"                                                                                                                                 
## [255] "F1112_F1A.Long.term.debt..current.portion"                                                                                                              
## [256] "F1112_F1A.Other.current.liabilities"                                                                                                                    
## [257] "F1112_F1A.Total.current.liabilities"                                                                                                                    
## [258] "F1112_F1A.Long.term.debt"                                                                                                                               
## [259] "F1112_F1A.Other.noncurrent.liabilities"                                                                                                                 
## [260] "F1112_F1A.Total.noncurrent.liabilities"                                                                                                                 
## [261] "F1112_F1A.Total.liabilities"                                                                                                                            
## [262] "F1112_F1A.Invested.in.capital.assets..net.of.related.debt"                                                                                              
## [263] "F1112_F1A.Restricted.expendable"                                                                                                                        
## [264] "F1112_F1A.Restricted.nonexpendable"                                                                                                                     
## [265] "F1112_F1A.Unrestricted"                                                                                                                                 
## [266] "F1112_F1A.Total.net.assets"                                                                                                                             
## [267] "F1112_F1A.Land..improvements...Ending.balance"                                                                                                          
## [268] "F1112_F1A.Infrastructure...Ending.balance"                                                                                                              
## [269] "F1112_F1A.Buildings...Ending.balance"                                                                                                                   
## [270] "F1112_F1A.Equipment..including.art.and.library.collections...Ending.balance"                                                                            
## [271] "F1112_F1A.Construction.in.progress...Ending.balance"                                                                                                    
## [272] "F1112_F1A.Total.for.plant..property.and.equipment...Ending.balance"                                                                                     
## [273] "F1112_F1A.Accumulated.depreciation...Ending.balance"                                                                                                    
## [274] "F1112_F1A.Intangible.assets...net.of.accumulated.amortization...Ending.balance"                                                                         
## [275] "F1112_F1A.Other.capital.assets...Ending.balance..New.Aligned."                                                                                          
## [276] "F1112_F1A.Tuition.and.fees..after.deducting.discounts.and.allowances"                                                                                   
## [277] "F1112_F1A.Federal.operating.grants.and.contracts"                                                                                                       
## [278] "F1112_F1A.State.operating.grants.and.contracts"                                                                                                         
## [279] "F1112_F1A.Local.private.operating.grants.and.contracts"                                                                                                 
## [280] "F1112_F1A.Local.operating.grants.and.contracts"                                                                                                         
## [281] "F1112_F1A.Private.operating.grants.and.contracts"                                                                                                       
## [282] "F1112_F1A.Sales.and.services.of.auxiliary.enterprises"                                                                                                  
## [283] "F1112_F1A.Sales.and.services.of.hospitals"                                                                                                              
## [284] "F1112_F1A.Sales.and.services.of.educational.activities"                                                                                                 
## [285] "F1112_F1A.Independent.operations"                                                                                                                       
## [286] "F1112_F1A.Other.sources...operating"                                                                                                                    
## [287] "F1112_F1A.Total.operating.revenues"                                                                                                                     
## [288] "F1112_F1A.Federal.appropriations"                                                                                                                       
## [289] "F1112_F1A.State.appropriations"                                                                                                                         
## [290] "F1112_F1A.Local.appropriations..education.district.taxes..and.similar.support"                                                                          
## [291] "F1112_F1A.Federal.nonoperating.grants"                                                                                                                  
## [292] "F1112_F1A.State.nonoperating.grants"                                                                                                                    
## [293] "F1112_F1A.Local.nonoperating.grants"                                                                                                                    
## [294] "F1112_F1A.Gifts..including.contributions.from.affiliated.organizations"                                                                                 
## [295] "F1112_F1A.Investment.income"                                                                                                                            
## [296] "F1112_F1A.Other.nonoperating.revenues"                                                                                                                  
## [297] "F1112_F1A.Total.nonoperating.revenues"                                                                                                                  
## [298] "F1112_F1A.Total.operating.and.nonoperating.revenues"                                                                                                    
## [299] "F1112_F1A.Capital.appropriations"                                                                                                                       
## [300] "F1112_F1A.Capital.grants.and.gifts"                                                                                                                     
## [301] "F1112_F1A.Additions.to.permanent.endowments"                                                                                                            
## [302] "F1112_F1A.Other.revenues.and.additions"                                                                                                                 
## [303] "F1112_F1A.Total.other.revenues.and.additions"                                                                                                           
## [304] "F1112_F1A.Total.all.revenues.and.other.additions"                                                                                                       
## [305] "F1112_F1A.Instruction...Current.year.total"                                                                                                             
## [306] "F1112_F1A.Instruction...Salaries.and.wages"                                                                                                             
## [307] "F1112_F1A.Instruction...Employee.fringe.benefits"                                                                                                       
## [308] "F1112_F1A.Instruction...Operations.and.maintenance.of.plant"                                                                                            
## [309] "F1112_F1A.Instruction...Depreciation"                                                                                                                   
## [310] "F1112_F1A.Instruction...Interest"                                                                                                                       
## [311] "F1112_F1A.Instruction...All.other"                                                                                                                      
## [312] "F1112_F1A.Research...Current.year.total"                                                                                                                
## [313] "F1112_F1A.Research...Salaries.and.wages"                                                                                                                
## [314] "F1112_F1A.Research...Employee.fringe.benefits"                                                                                                          
## [315] "F1112_F1A.Research...Operations.and.maintenance.of.plant"                                                                                               
## [316] "F1112_F1A.Research...Depreciation"                                                                                                                      
## [317] "F1112_F1A.Research...Interest"                                                                                                                          
## [318] "F1112_F1A.Research...All.other"                                                                                                                         
## [319] "F1112_F1A.Public.service...Current.year.total"                                                                                                          
## [320] "F1112_F1A.Public.service...Salaries.and.wages"                                                                                                          
## [321] "F1112_F1A.Public.service...Employee.fringe.benefits"                                                                                                    
## [322] "F1112_F1A.Public.service...Operations.and.maintenance.of.plant"                                                                                         
## [323] "F1112_F1A.Public.service...Depreciation"                                                                                                                
## [324] "F1112_F1A.Public.service...Interest"                                                                                                                    
## [325] "F1112_F1A.Public.service...All.other"                                                                                                                   
## [326] "F1112_F1A.Academic.support...Current.year.total"                                                                                                        
## [327] "F1112_F1A.Academic.support...Salaries.and.wages"                                                                                                        
## [328] "F1112_F1A.Academic.support...Employee.fringe.benefits"                                                                                                  
## [329] "F1112_F1A.Academic.support...Operations.and.maintenance.of.plant"                                                                                       
## [330] "F1112_F1A.Academic.support...Depreciation"                                                                                                              
## [331] "F1112_F1A.Academic.support...Interest"                                                                                                                  
## [332] "F1112_F1A.Academic.support...All.other"                                                                                                                 
## [333] "F1112_F1A.Student.services...Current.year.total"                                                                                                        
## [334] "F1112_F1A.Student.services...Salaries.and.wages"                                                                                                        
## [335] "F1112_F1A.Student.services...Employee.fringe.benefits"                                                                                                  
## [336] "F1112_F1A.Student.services...Operations.and.maintenance.of.plant"                                                                                       
## [337] "F1112_F1A.Student.services...Depreciation"                                                                                                              
## [338] "F1112_F1A.Student.services...Interest"                                                                                                                  
## [339] "F1112_F1A.Student.services...All.other"                                                                                                                 
## [340] "F1112_F1A.Institutional.support...Current.year.total"                                                                                                   
## [341] "F1112_F1A.Institutional.support...Salaries.and.wages"                                                                                                   
## [342] "F1112_F1A.Institutional.support...Employee.fringe.benefits"                                                                                             
## [343] "F1112_F1A.Institutional.support...Operations.and.maintenance.of.plant"                                                                                  
## [344] "F1112_F1A.Institutional.support...Depreciation"                                                                                                         
## [345] "F1112_F1A.Institutional.support...Interest"                                                                                                             
## [346] "F1112_F1A.Institutional.support...All.other"                                                                                                            
## [347] "F1112_F1A.Operation..maintenance.of.plant...Current.year.total"                                                                                         
## [348] "F1112_F1A.Operation..maintenance.of.plant...Salaries.and.wages"                                                                                         
## [349] "F1112_F1A.Operation..maintenance.of.plant...Employee.fringe.benefits"                                                                                   
## [350] "F1112_F1A.Operation.maintenance.of.plant...Operation.and.maintenance.of.plant"                                                                          
## [351] "F1112_F1A.Operation..maintenance.of.plant...Depreciation"                                                                                               
## [352] "F1112_F1A.Operation.maintenance.of.plant...Interest"                                                                                                    
## [353] "F1112_F1A.Operation..maintenance.of.plant...All.other"                                                                                                  
## [354] "F1112_F1A.Scholarships.and.fellowships.expenses....Current.year.total"                                                                                  
## [355] "F1112_F1A.Scholarships.and.fellowships.expenses....All.other"                                                                                           
## [356] "F1112_F1A.Auxiliary.enterprises....Current.year.total"                                                                                                  
## [357] "F1112_F1A.Auxiliary.enterprises....Salaries.and.wages"                                                                                                  
## [358] "F1112_F1A.Auxiliary.enterprises....Employee.fringe.benefits"                                                                                            
## [359] "F1112_F1A.Auxiliary.enterprises....Operations.and.maintenance.of.plant"                                                                                 
## [360] "F1112_F1A.Auxiliary.enterprises....Depreciation"                                                                                                        
## [361] "F1112_F1A.Auxiliary.enterprises...Interest"                                                                                                             
## [362] "F1112_F1A.Auxiliary.enterprises....All.other"                                                                                                           
## [363] "F1112_F1A.Hospital.services...Current.year.total"                                                                                                       
## [364] "F1112_F1A.Hospital.services...Salaries.and.wages"                                                                                                       
## [365] "F1112_F1A.Hospital.services...Employee.fringe.benefits"                                                                                                 
## [366] "F1112_F1A.Hospital.services....Operations.and.maintenance.of.plant"                                                                                     
## [367] "F1112_F1A.Hospital.services...Depreciation"                                                                                                             
## [368] "F1112_F1A.Hospital.services...Interest"                                                                                                                 
## [369] "F1112_F1A.Hospital.services...All.other"                                                                                                                
## [370] "F1112_F1A.Independent.operations...Current.year.total"                                                                                                  
## [371] "F1112_F1A.Independent.operations...Salaries.and.wages"                                                                                                  
## [372] "F1112_F1A.Independent.operations...Employee.fringe.benefits"                                                                                            
## [373] "F1112_F1A.Independent.operations....Operations.and.maintenance.of.plant"                                                                                
## [374] "F1112_F1A.Independent.operations...Depreciation"                                                                                                        
## [375] "F1112_F1A.Independent.operations...Interest"                                                                                                            
## [376] "F1112_F1A.Independent.operations...All.other"                                                                                                           
## [377] "F1112_F1A.Other.expenses..deductions...Current.year.total"                                                                                              
## [378] "F1112_F1A.Other.expenses..deductions...Salaries.and.wages"                                                                                              
## [379] "F1112_F1A.Other.expenses..deductions...Employee.fringe.benefits"                                                                                        
## [380] "F1112_F1A.Other.expenses.deductions....Operations.and.maintenance.of.plant"                                                                             
## [381] "F1112_F1A.Other.expenses..deductions...Depreciation"                                                                                                    
## [382] "F1112_F1A.Other.expenses.deductions...Interest"                                                                                                         
## [383] "F1112_F1A.Other.expenses..deductions...All.other"                                                                                                       
## [384] "F1112_F1A.Total.expenses..deductions...Current.year.total"                                                                                              
## [385] "F1112_F1A.Total.expenses..deductions...Salaries.and.wages"                                                                                              
## [386] "F1112_F1A.Total.expenses..deductions...Employee.fringe.benefits"                                                                                        
## [387] "F1112_F1A.Total.expenses.deductions...Operations.and.maintenance.of.plant"                                                                              
## [388] "F1112_F1A.Total.expenses..deductions...Depreciation"                                                                                                    
## [389] "F1112_F1A.Total.expenses.deductions...Interest"                                                                                                         
## [390] "F1112_F1A.Total.expenses..deductions...All.other"                                                                                                       
## [391] "F1112_F1A.Total.revenues.and.other.additions"                                                                                                           
## [392] "F1112_F1A.Total.expenses.and.other.deductions"                                                                                                          
## [393] "F1112_F1A.Increase.in.net.assets.during.the.year"                                                                                                       
## [394] "F1112_F1A.Net.assets.beginning.of.year"                                                                                                                 
## [395] "F1112_F1A.Adjustments.to.beginning.net.assets"                                                                                                          
## [396] "F1112_F1A.Net.assets.end.of.year"                                                                                                                       
## [397] "F1112_F1A.Pell.grants..federal."                                                                                                                        
## [398] "F1112_F1A.Other.federal.grants"                                                                                                                         
## [399] "F1112_F1A.Grants.by.state.government"                                                                                                                   
## [400] "F1112_F1A.Grants.by.local.government"                                                                                                                   
## [401] "F1112_F1A.Institutional.grants.from.restricted.resources"                                                                                               
## [402] "F1112_F1A.Institutional.grants.from.unrestricted.resources"                                                                                             
## [403] "F1112_F1A.Total.gross.scholarships.and.fellowships"                                                                                                     
## [404] "F1112_F1A.Discounts.and.allowances.applied.to.tuition.and.fees"                                                                                         
## [405] "F1112_F1A.Discounts.and.allowances.applied.to.sales...services.of.auxiliary.enterprises"                                                                
## [406] "F1112_F1A.Total.discounts.and.allowances"                                                                                                               
## [407] "F1112_F1A.Net.scholarships.and.fellowship.expenses"                                                                                                     
## [408] "F1112_F1A.Does.this.institution.or.any.of.its.foundations.or.other.affiliated.organizations.own.endowment.assets.."                                     
## [409] "F1112_F1A.Value.of.endowment.assets.at.the.beginning.of.the.fiscal.year"                                                                                
## [410] "F1112_F1A.Value.of.endowment.assets.at.the.end.of.the.fiscal.year"                                                                                      
## [411] "DRVF2012.Core.revenues..total.dollars..GASB."                                                                                                           
## [412] "DRVF2012.Tuition.and.fees.as.a.percent.of.core.revenues..GASB."                                                                                         
## [413] "DRVF2012.State.appropriations.as.percent.of.core.revenues...GASB."                                                                                      
## [414] "DRVF2012.Local.appropriations.as.a.percent.of.core.revenues..GASB."                                                                                     
## [415] "DRVF2012.Government.grants.and.contracts.as.a.percent.of.core.revenues..GASB."                                                                          
## [416] "DRVF2012.Private.gifts..grants..and.contracts.as.a.percent.of.core.revenues..GASB."                                                                     
## [417] "DRVF2012.Investment.return.as.a.percent.of.core.revenues..GASB."                                                                                        
## [418] "DRVF2012.Other.revenues.as.a.percent.of.core.revenues..GASB."                                                                                           
## [419] "DRVF2012.Core.revenues..total.dollars..FASB."                                                                                                           
## [420] "DRVF2012.Tuition.and.fees.as.a.percent.of.core.revenues..FASB."                                                                                         
## [421] "DRVF2012.Government.grants.and.contracts.as.a.percent.of.core.revenues..FASB."                                                                          
## [422] "DRVF2012.Private.gifts..grants..contracts.contributions.from.affiliated.entities.as.a.percent.of.core.revenues..FASB."                                  
## [423] "DRVF2012.Investment.return.as.a.percent.of.core.revenues..FASB."                                                                                        
## [424] "DRVF2012.Other.revenues.as.a.percent.of.core.revenues..FASB."                                                                                           
## [425] "DRVF2012.Core.revenues..total.dollars..for.profit.institutions."                                                                                        
## [426] "DRVF2012.Tuition.and.fees.as.a.percent.of.core.revenues..for.profit.institutions."                                                                      
## [427] "DRVF2012.Govenment.appropriations..grants..and.contracts.as.a.percent.of.core.revenues..for.profit.institutions."                                       
## [428] "DRVF2012.Sales.and.services.of.educational.activities.as.a.percent.of.core.revenues..for.profit.institutions."                                          
## [429] "DRVF2012.Other.revenues.as.a.percent.of.core.revenues..for.profit.institutions."                                                                        
## [430] "DRVF2012.Revenues.from.tuition.and.fees.per.FTE..GASB."                                                                                                 
## [431] "DRVF2012.Revenues.from.state.appropriations.per.FTE..GASB."                                                                                             
## [432] "DRVF2012.Revenues.from.local.appropriations.per.FTE..GASB."                                                                                             
## [433] "DRVF2012.Revenues.from.government.grants.and.contracts.per.FTE..GASB."                                                                                  
## [434] "DRVF2012.Revenues.from.private.gifts..grants..and.contracts.per.FTE..GASB."                                                                             
## [435] "DRVF2012.Revenues.from.investment.return.per.FTE..GASB."                                                                                                
## [436] "DRVF2012.Other.core.revenues.per.FTE..GASB."                                                                                                            
## [437] "DRVF2012.Revenues.from.tuition.and.fees.per.FTE..FASB."                                                                                                 
## [438] "DRVF2012.Revenues.from.government.grants.and.contracts.per.FTE..FASB."                                                                                  
## [439] "DRVF2012.Revenues.from.private.gifts..grants..contracts.contributions.from.affiliated.entities.per.FTE..FASB."                                          
## [440] "DRVF2012.Revenues.from.investment.return.per.FTE..FASB."                                                                                                
## [441] "DRVF2012.Other.core.revenues.per.FTE..FASB."                                                                                                            
## [442] "DRVF2012.Revenues.from.tuition.and.fees.per.FTE..for.profit.institutions."                                                                              
## [443] "DRVF2012.Revenues.from.government.appropriations..grants.and.contracts.per.FTE..for.profit.institutions."                                               
## [444] "DRVF2012.Revenues.from.sales.and.services.of.educational.activities.per.FTE...for.profit.institutions."                                                 
## [445] "DRVF2012.Other.core.revenues.per.FTE..for.profit.institutions."                                                                                         
## [446] "DRVF2012.Core.expenses..total.dollars..GASB."                                                                                                           
## [447] "DRVF2012.Instruction.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                               
## [448] "DRVF2012.Research.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                                  
## [449] "DRVF2012.Public.service.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                            
## [450] "DRVF2012.Academic.support.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                          
## [451] "DRVF2012.Student.service.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                           
## [452] "DRVF2012.Institutional.support.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                     
## [453] "DRVF2012.Other.core.expenses.as.a.percent.of.total.core.expenses..GASB."                                                                                
## [454] "DRVF2012.Core.expenses..total.dollars..FASB."                                                                                                           
## [455] "DRVF2012.Instruction.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                               
## [456] "DRVF2012.Research.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                                  
## [457] "DRVF2012.Public.service.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                            
## [458] "DRVF2012.Academic.support.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                          
## [459] "DRVF2012.Student.service.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                           
## [460] "DRVF2012.Institutional.support.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                     
## [461] "DRVF2012.Other.core.expenses.as.a.percent.of.total.core.expenses..FASB."                                                                                
## [462] "DRVF2012.Core.expenses..total.dollars..for.profit.institutons."                                                                                         
## [463] "DRVF2012.Instruction.expenses.as.a.percent.of.total.core.expenses..for.profit.institutions."                                                            
## [464] "DRVF2012.Academic.and.institutional.support..and.student.service.expenses.as.a.percent.of.total.core.expenses..for.profit.institutions."                
## [465] "DRVF2012.Other.core.expenses.as.a.percent.of.total..core.expenses..for.profit.institutions."                                                            
## [466] "DRVF2012.Instruction.expenses.per.FTE...GASB."                                                                                                          
## [467] "DRVF2012.Research.expenses.per.FTE...GASB."                                                                                                             
## [468] "DRVF2012.Public.service.expenses.per.FTE..GASB."                                                                                                        
## [469] "DRVF2012.Academic.support.expenses.per.FTE..GASB."                                                                                                      
## [470] "DRVF2012.Student.service.expenses.per.FTE..GASB."                                                                                                       
## [471] "DRVF2012.Institutional.support.expenses.per.FTE..GASB."                                                                                                 
## [472] "DRVF2012.All.other.core.expenses.per.FTE..GASB."                                                                                                        
## [473] "DRVF2012.Instruction.expenses.per.FTE...FASB."                                                                                                          
## [474] "DRVF2012.Research.expenses.per.FTE..FASB."                                                                                                              
## [475] "DRVF2012.Public.service.expenses.per.FTE..FASB."                                                                                                        
## [476] "DRVF2012.Academic.support.expenses.per.FTE..FASB."                                                                                                      
## [477] "DRVF2012.Student.service.expenses.per.FTE..FASB."                                                                                                       
## [478] "DRVF2012.Institutional.support.expenses.per.FTE..FASB."                                                                                                 
## [479] "DRVF2012.All.other.core.expenses.per.FTE..FASB."                                                                                                        
## [480] "DRVF2012.Instruction.expenses.per.FTE..for.profit.institutions."                                                                                        
## [481] "DRVF2012.Academic.and.institutional.support..and.student.services..expense.per.FTE..for.profit.institutions."                                           
## [482] "DRVF2012.All.other.core.expenses.per.FTE..for.profit.institutions."                                                                                     
## [483] "DRVF2012.Salaries..wages..and.benefit.expenses.for.core.expenses.as.a.percent.of.total.core.expenses..GASB."                                            
## [484] "DRVF2012.Salaries..wages..and.benefit.expenses.for.instruction.as.a.percent.of.total.expenses.for.instruction..GASB."                                   
## [485] "DRVF2012.Salaries..wages..and.benefit.expenses.for.research.as.a.percent.of.total.expenses.for.research..GASB."                                         
## [486] "DRVF2012.Salaries..wages..and.benefit.expenses.for.public.service.as.a.percent.of.total.expenses.for.public.service..GASB."                             
## [487] "DRVF2012.Salaries..wages..and.benefit.expenses.for.academic.support.as.a.percent.of.total.expenses.for.academic.support..GASB."                         
## [488] "DRVF2012.Salaries..wages..and.benefit.expenses.for.student.services.as.a.percent.of.total.expenses.for.student.services..GASB."                         
## [489] "DRVF2012.Salaries..wages..and.benefit.expenses.for.institutional.support.as.a.percent.of.total.expenses.for.institutional.support..GASB."               
## [490] "DRVF2012.Salaries..wages..and.benefit.expenses.for.other.core.expense.functions..as.a.percent.of.total.expenses.for.other.core.expense.functions..GASB."
## [491] "DRVF2012.Total.salaries..wages..and.benefit.expenses.as.a.percent.of.total.expenses..GASB."                                                             
## [492] "DRVF2012.Total.salaries.and.wage.expenses.as.a.percent.of.total.expenses..GASB."                                                                        
## [493] "DRVF2012.Salaries..wages..and.benefit.expenses.for.core.expenses.as.a.percent.of.total.core.expenses..FASB."                                            
## [494] "DRVF2012.Salaries..wages..and.benefit.expenses.for.instruction.as.a.percent.of.total.expenses.for.instruction..FASB."                                   
## [495] "DRVF2012.Salaries..wages..and.benefit.expenses.for.research.as.a.percent.of.total.expenses.for.research..FASB."                                         
## [496] "DRVF2012.Salaries..wages..and.benefit.expenses.for.public.service.as.a.percent.of.total.expenses.for.public.service..FASB."                             
## [497] "DRVF2012.Salaries..wages..and.benefit.expenses.for.academic.support.as.a.percent.of.total.expenses.for.academic.support..FASB."                         
## [498] "DRVF2012.Salaries..wages..and.benefit.expenses.for.student.services.as.a.percent.of.total.expenses.for.student.services..FASB."                         
## [499] "DRVF2012.Salaries..wages..and.benefit.expenses.for.institutional.support.as.a.percent.of.total.expenses.for.institutional.support..FASB."               
## [500] "DRVF2012.Salaries..wages..and.benefit.expenses.for.other.core.expense.functions..as.a.percent.of.total.expenses.for.other.core.expense.functions..FASB."
## [501] "DRVF2012.Total.salaries..wages..and.benefit.expenses.as.a.percent.of.total.expenses..FASB."                                                             
## [502] "DRVF2012.Total.salaries.and.wage.expenses.as.a.percent.of.total.expenses..FASB."                                                                        
## [503] "DRVF2012.Endowment.assets..year.end..per.FTE.enrollment..GASB."                                                                                         
## [504] "DRVF2012.Endowment.assets..year.end..per.FTE.enrollment..FASB."                                                                                         
## [505] "DRVF2012.Equity.ratio..GASB."                                                                                                                           
## [506] "DRVF2012.Equity.ratio..FASB."                                                                                                                           
## [507] "DRVF2012.Equity.ratio..for.profit.institutions."
```

```r
# str(df7)
```



Category 8: Instructional staff / salaries
------------------------------------------


```r
df8_1 <- read.csv("2012/raw/08_Instructional_staff_salaries_1.csv")
dim(df8_1)
```

```
## [1] 1796   29
```

```r
names(df8_1)
```

```
##  [1] "unitid"                                                                
##  [2] "institution.name"                                                      
##  [3] "year"                                                                  
##  [4] "SAL2012_IS.Academic.rank"                                              
##  [5] "SAL2012_IS.Instructional.staff.on.9..10..11.or.12.month.contract.total"
##  [6] "SAL2012_IS.Instructional.staff.on.9..10..11.or.12.month.contract.men"  
##  [7] "SAL2012_IS.Instructional.staff.on.9..10..11.or.12.month.contract.women"
##  [8] "SAL2012_IS.Instructional.staff.on.9.month.contract.total"              
##  [9] "SAL2012_IS.Instructional.staff.on.9.month.contract.men"                
## [10] "SAL2012_IS.Instructional.staff.on.9.month.contract.women"              
## [11] "SAL2012_IS.Instructional.staff.on.10.month.contract.total"             
## [12] "SAL2012_IS.Instructional.staff.on.10.month.contract.men"               
## [13] "SAL2012_IS.Instructional.staff.on.10.month.contract.women"             
## [14] "SAL2012_IS.Instructional.staff.on.11.month.contract.total"             
## [15] "SAL2012_IS.Instructional.staff.on.11.month.contract.men"               
## [16] "SAL2012_IS.Instructional.staff.on.11.month.contract.women"             
## [17] "SAL2012_IS.Instructional.staff.on.12.month.contract.total"             
## [18] "SAL2012_IS.Instructional.staff.on.12.month.contract.men"               
## [19] "SAL2012_IS.Instructional.staff.on.12..month.contract.women"            
## [20] "SAL2012_IS.Number.months.covered.for.salary.outlays...total"           
## [21] "SAL2012_IS.Number.of.months.covered.for.salary.outlays...men"          
## [22] "SAL2012_IS.Number.of.months.covered.for.salary.outlays...women"        
## [23] "SAL2012_IS.Salary.outlays...total"                                     
## [24] "SAL2012_IS.Salary.outlays...men"                                       
## [25] "SAL2012_IS.Salary.outlays...women"                                     
## [26] "SAL2012_IS.Average.weighted.monthly.salary....total"                   
## [27] "SAL2012_IS.Average.weighted.monthly.salary....men"                     
## [28] "SAL2012_IS.Average.weighted.monthly.salary....women"                   
## [29] "IDX_HR"
```

```r
# str(df8_1)

df8_2 <- read.csv("2012/raw/08_Instructional_staff_salaries_2.csv")
dim(df8_2)
```

```
## [1] 380  49
```

```r
names(df8_2)
```

```
##  [1] "unitid"                                                                                              
##  [2] "institution.name"                                                                                    
##  [3] "year"                                                                                                
##  [4] "FLAGS2012.Response.status.to.SA.survey"                                                              
##  [5] "FLAGS2012.Salary.exclusion"                                                                          
##  [6] "FLAGS2012.Parent.child.allocation.factor...HR"                                                       
##  [7] "FLAGS2012.Does.institution.have.a.tenure.system"                                                     
##  [8] "DRVC2012.Number.of.students.receiving.a.certificate.of.less.than.1.year"                             
##  [9] "FLAGS2012.Natural.Disaster.identification"                                                           
## [10] "FLAGS2012.Response.status.of.institution.for.Human.Resources..HR..component"                         
## [11] "FLAGS2012.Type.of.Imputation.method...Human.Resources..HR..component"                                
## [12] "FLAGS2012.Status.of.Human.Resources..HR..component.when.data.collection.closed"                      
## [13] "FLAGS2012.Parent.child..indicator...Human.Resources..HR..component"                                  
## [14] "FLAGS2012.ID.of.institution.where.data.are.reported.for.the.Human.Resources..HR..component"          
## [15] "SAL2012_NIS.Full.time.non.instructional.staff...number"                                              
## [16] "SAL2012_NIS.Full.time.non.instructional.staff...outlays"                                             
## [17] "SAL2012_NIS.Postsecondary.Teachers...Research...number"                                              
## [18] "SAL2012_NIS.Postsecondary.Teachers...Research...outlays"                                             
## [19] "SAL2012_NIS.Postsecondary.Teachers...Public.service...number"                                        
## [20] "SAL2012_NIS.Postsecondary.Teachers...Public.service.Outlays"                                         
## [21] "SAL2012_NIS.Librarians..Curators..Archivists..other.teaching.and.Instructional.support....number"    
## [22] "SAL2012_NIS.Librarians..Curators..Archivists..other.teaching.and.Instructional.support....outlays"   
## [23] "SAL2012_NIS.Management...number"                                                                     
## [24] "SAL2012_NIS.Management...outlays"                                                                    
## [25] "SAL2012_NIS.Business.and.Financial.Operations...number"                                              
## [26] "SAL2012_NIS.Business.and.Financial.Operations...outlays"                                             
## [27] "SAL2012_NIS.Computer..Engineering..and.Science...number"                                             
## [28] "SAL2012_NIS.Computer..Engineering..and.Science...outlays"                                            
## [29] "SAL2012_NIS.Community.Service..Legal..Arts..and.Media...number"                                      
## [30] "SAL2012_NIS.Community.Service..Legal..Arts..and.Media...outlays"                                     
## [31] "SAL2012_NIS.Healthcare.Practioners.and.Technical..number"                                            
## [32] "SAL2012_NIS.Healthcare.Practioners.and.Technical...outlays"                                          
## [33] "SAL2012_NIS.Service...number"                                                                        
## [34] "SAL2012_NIS.Service...outlays"                                                                       
## [35] "SAL2012_NIS.Sales.and.related...number"                                                              
## [36] "SAL2012_NIS.Sales.and.related...outlays"                                                             
## [37] "SAL2012_NIS.Office.and.Administrative.Support...number"                                              
## [38] "SAL2012_NIS.Office.and.Administrative.Support...outlays"                                             
## [39] "SAL2012_NIS.Natural.Resources..Construction..and.Maintenance...number"                               
## [40] "SAL2012_NIS.Natural.Resources..Construction..and.Maintenance...outlays"                              
## [41] "SAL2012_NIS.Production..Transportation..and.Material.Moving...number"                                
## [42] "SAL2012_NIS.Production..Transportation..and.Material.Moving...outlays"                               
## [43] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...all.ranks"           
## [44] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.insructional.staff...professors"           
## [45] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...associate.professors"
## [46] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...assistant.professors"
## [47] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...instructors"         
## [48] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...lecturers"           
## [49] "DRVHR2012.Average.salary.equated.to.9.months.of.full.time.instructional.staff...No.academic.rank"
```

```r
# str(df8_2)
```



Category 9: Fall staff
------------------------------------------


```r
df9_1 <- read.csv("2012/raw/09_Fall_staff_1.csv")
dim(df9_1)
```

```
## [1] 2899   35
```

```r
names(df9_1)
```

```
##  [1] "unitid"                                                  
##  [2] "institution.name"                                        
##  [3] "year"                                                    
##  [4] "S2012_NH.Staff.category"                                 
##  [5] "S2012_NH.Grand.total"                                    
##  [6] "S2012_NH.Grand.total.men"                                
##  [7] "S2012_NH.Grand.total.women"                              
##  [8] "S2012_NH.American.Indian.or.Alaska.Native.total"         
##  [9] "S2012_NH.American.Indian.or.Alaska.Native.men"           
## [10] "S2012_NH.American.Indian.or.Alaska.Native.women"         
## [11] "S2012_NH.Asian.total"                                    
## [12] "S2012_NH.Asian.men"                                      
## [13] "S2012_NH.Asian.women"                                    
## [14] "S2012_NH.Black.or.African.American.total"                
## [15] "S2012_NH.Black.or.African.American.men"                  
## [16] "S2012_NH.Black.or.African.American.women"                
## [17] "S2012_NH.Hispanic.or.Latino.total"                       
## [18] "S2012_NH.Hispanic.or.Latino.men"                         
## [19] "S2012_NH.Hispanic.or.Latino.women"                       
## [20] "S2012_NH.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "S2012_NH.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "S2012_NH.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "S2012_NH.White.total"                                    
## [24] "S2012_NH.White.men"                                      
## [25] "S2012_NH.White.women"                                    
## [26] "S2012_NH.Two.or.more.races.total"                        
## [27] "S2012_NH.Two.or.more.races.men"                          
## [28] "S2012_NH.Two.or.more.races.women"                        
## [29] "S2012_NH.Race.ethnicity.unknown.total"                   
## [30] "S2012_NH.Race.ethnicity.unknown.men"                     
## [31] "S2012_NH.Race.ethnicity.unknown.women"                   
## [32] "S2012_NH.Nonresident.alien.total"                        
## [33] "S2012_NH.Nonresident.alien.men"                          
## [34] "S2012_NH.Nonresident.alien.women"                        
## [35] "IDX_HR"
```

```r
# str(df9_1)

df9_2 <- read.csv("2012/raw/09_Fall_staff_2.csv")
dim(df9_2)
```

```
## [1] 2159   12
```

```r
names(df9_2)
```

```
##  [1] "unitid"                             
##  [2] "institution.name"                   
##  [3] "year"                               
##  [4] "S2012_SIS.Faculty.and.tenure.status"
##  [5] "S2012_SIS.All.ranks"                
##  [6] "S2012_SIS.Professors"               
##  [7] "S2012_SIS.Associate.professors"     
##  [8] "S2012_SIS.Assistant.professors"     
##  [9] "S2012_SIS.Intructors"               
## [10] "S2012_SIS.Lecturers"                
## [11] "S2012_SIS.No.academic.rank"         
## [12] "IDX_HR"
```

```r
# str(df9_2)

df9_3 <- read.csv("2012/raw/09_Fall_staff_3.csv")
dim(df9_3)
```

```
## [1] 11116    35
```

```r
names(df9_3)
```

```
##  [1] "unitid"                                                  
##  [2] "institution.name"                                        
##  [3] "year"                                                    
##  [4] "S2012_OC.Occupation.and.full..and.part.time.status"      
##  [5] "S2012_OC.Grand.total"                                    
##  [6] "S2012_OC.Grand.total.men"                                
##  [7] "S2012_OC.Grand.total.women"                              
##  [8] "S2012_OC.American.Indian.or.Alaska.Native.total"         
##  [9] "S2012_OC.American.Indian.or.Alaska.Native.men"           
## [10] "S2012_OC.American.Indian.or.Alaska.Native.women"         
## [11] "S2012_OC.Asian.total"                                    
## [12] "S2012_OC.Asian.men"                                      
## [13] "S2012_OC.Asian.women"                                    
## [14] "S2012_OC.Black.or.African.American.total"                
## [15] "S2012_OC.Black.or.African.American.men"                  
## [16] "S2012_OC.Black.or.African.American.women"                
## [17] "S2012_OC.Hispanic.or.Latino.total"                       
## [18] "S2012_OC.Hispanic.or.Latino.men"                         
## [19] "S2012_OC.Hispanic.or.Latino.women"                       
## [20] "S2012_OC.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "S2012_OC.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "S2012_OC.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "S2012_OC.White.total"                                    
## [24] "S2012_OC.White.men"                                      
## [25] "S2012_OC.White.women"                                    
## [26] "S2012_OC.Two.or.more.races.total"                        
## [27] "S2012_OC.Two.or.more.races.men"                          
## [28] "S2012_OC.Two.or.more.races.women"                        
## [29] "S2012_OC.Race.ethnicity.unknown.total"                   
## [30] "S2012_OC.Race.ethnicity.unknown.men"                     
## [31] "S2012_OC.Race.ethnicity.unknown.women"                   
## [32] "S2012_OC.Nonresident.alien.total"                        
## [33] "S2012_OC.Nonresident.alien.men"                          
## [34] "S2012_OC.Nonresident.alien.women"                        
## [35] "IDX_HR"
```

```r
# str(df9_3)

df9_4 <- read.csv("2012/raw/09_Fall_staff_4.csv")
dim(df9_4)
```

```
## [1] 5305   35
```

```r
names(df9_4)
```

```
##  [1] "unitid"                                                  
##  [2] "institution.name"                                        
##  [3] "year"                                                    
##  [4] "S2012_IS.Instructional.staff.category"                   
##  [5] "S2012_IS.Grand.total"                                    
##  [6] "S2012_IS.Grand.total.men"                                
##  [7] "S2012_IS.Grand.total.women"                              
##  [8] "S2012_IS.American.Indian.or.Alaska.Native.total"         
##  [9] "S2012_IS.American.Indian.or.Alaska.Native.men"           
## [10] "S2012_IS.American.Indian.or.Alaska.Native.women"         
## [11] "S2012_IS.Asian.total"                                    
## [12] "S2012_IS.Asian.men"                                      
## [13] "S2012_IS.Asian.women"                                    
## [14] "S2012_IS.Black.or.African.American.total"                
## [15] "S2012_IS.Black.or.African.American.men"                  
## [16] "S2012_IS.Black.or.African.American.women"                
## [17] "S2012_IS.Hispanic.or.Latino.total"                       
## [18] "S2012_IS.Hispanic.or.Latino.men"                         
## [19] "S2012_IS.Hispanic.or.Latino.women"                       
## [20] "S2012_IS.Native.Hawaiian.or.Other.Pacific.Islander.total"
## [21] "S2012_IS.Native.Hawaiian.or.Other.Pacific.Islander.men"  
## [22] "S2012_IS.Native.Hawaiian.or.Other.Pacific.Islander.women"
## [23] "S2012_IS.White.total"                                    
## [24] "S2012_IS.White.men"                                      
## [25] "S2012_IS.White.women"                                    
## [26] "S2012_IS.Two.or.more.races.total"                        
## [27] "S2012_IS.Two.or.more.races.men"                          
## [28] "S2012_IS.Two.or.more.races.women"                        
## [29] "S2012_IS.Race.ethnicity.unknown.total"                   
## [30] "S2012_IS.Race.ethnicity.unknown.men"                     
## [31] "S2012_IS.Race.ethnicity.unknown.women"                   
## [32] "S2012_IS.Nonresident.alien.total"                        
## [33] "S2012_IS.Nonresident.alien.men"                          
## [34] "S2012_IS.Nonresident.alien.women"                        
## [35] "IDX_HR"
```

```r
# str(df9_4)

df9_5 <- read.csv("2012/raw/09_Fall_staff_5.csv")
dim(df9_5)
```

```
## [1] 380  32
```

```r
names(df9_5)
```

```
##  [1] "unitid"                                                                                                                                         
##  [2] "institution.name"                                                                                                                               
##  [3] "year"                                                                                                                                           
##  [4] "FLAGS2012.Parent.child.allocation.factor...HR"                                                                                                  
##  [5] "FLAGS2012.Does.institution.have.a.tenure.system"                                                                                                
##  [6] "FLAGS2012.Does.institution.have.15.or.more.full.time.employees"                                                                                 
##  [7] "FLAGS2012.Natural.Disaster.identification"                                                                                                      
##  [8] "FLAGS2012.Response.status.for.Fall.Staff"                                                                                                       
##  [9] "FLAGS2012.Response.status.of.institution.for.Human.Resources..HR..component"                                                                    
## [10] "FLAGS2012.Type.of.Imputation.method...Human.Resources..HR..component"                                                                           
## [11] "FLAGS2012.Status.of.Human.Resources..HR..component.when.data.collection.closed"                                                                 
## [12] "FLAGS2012.Parent.child..indicator...Human.Resources..HR..component"                                                                             
## [13] "FLAGS2012.ID.of.institution.where.data.are.reported.for.the.Human.Resources..HR..component"                                                     
## [14] "DRVHR2012.Total.FTE.staff"                                                                                                                      
## [15] "DRVHR2012.Postsecondary.Teachers.FTE.staff"                                                                                                     
## [16] "DRVHR2012.Postsecondary.Teachers.Instructional.FTE"                                                                                             
## [17] "DRVHR2012.Postsecondary.Teachers.Research.FTE"                                                                                                  
## [18] "DRVHR2012.Postsecondary.Teachers.Public.Service.FTE"                                                                                            
## [19] "DRVHR2012.Librarians..Curators..and.Archivists.and.other.teaching.and.Instructional.support.occupations"                                        
## [20] "DRVHR2012.Librarians..Curators..and.Archivists.FTE"                                                                                             
## [21] "DRVHR2012.Other.teaching.and.Instructional.Support.FTE"                                                                                         
## [22] "DRVHR2012.Management.FTE"                                                                                                                       
## [23] "DRVHR2012.Business.and.Financial.Operations.FTE"                                                                                                
## [24] "DRVHR2012.Computer..Engineering..and.Science.FTE"                                                                                               
## [25] "DRVHR2012.Community.Service..Legal..Arts..and.Media.FTE"                                                                                        
## [26] "DRVHR2012.Healthcare.FTE"                                                                                                                       
## [27] "DRVHR2012.Service..sales..office.admin.support..natural.resources..construction..maintenance..production..transportation...materials.moving.FTE"
## [28] "DRVHR2012.Service.FTE"                                                                                                                          
## [29] "DRVHR2012.Sales.and.Related.FTE"                                                                                                                
## [30] "DRVHR2012.Office.and.Administrative.Support.FTE"                                                                                                
## [31] "DRVHR2012.Natural.Resources..Construction..and.Maintenance.FTE"                                                                                 
## [32] "DRVHR2012.Production..Transportation..and.Material.Moving.FTE"
```

```r
# str(df9_5)
```



Category 10: Employees by assigned position
-------------------------------------------


```r
df10_1 <- read.csv("2012/raw/10_Employees_by_assigned_position_1.csv")
dim(df10_1)
```

```
## [1] 26145    14
```

```r
names(df10_1)
```

```
##  [1] "unitid"                                                  
##  [2] "institution.name"                                        
##  [3] "year"                                                    
##  [4] "EAP2012.Occupation.and.faculty.tenure.status"            
##  [5] "EAP2012.Total.employees"                                 
##  [6] "EAP2012.Institution.employees..excluding.medical.school."
##  [7] "EAP2012.Medical.school.employees"                        
##  [8] "EAP2012.Full.time.employees"                             
##  [9] "EAP2012.Full.time.employees..excluding.medical.schools." 
## [10] "EAP2012.Full.time.employees..medical.school."            
## [11] "EAP2012.Part.time.employees"                             
## [12] "EAP2012.Part.time.employees..excluding.medical.schools." 
## [13] "EAP2012.Part.time.employees..medical.school."            
## [14] "IDX_HR"
```

```r
str(df10_1)
```

```
## 'data.frame':	26145 obs. of  14 variables:
##  $ unitid                                                  : int  125231 125231 125231 125231 125231 125231 125231 125231 125231 125231 ...
##  $ institution.name                                        : Factor w/ 378 levels "Adrian College",..: 357 357 357 357 357 357 357 357 357 357 ...
##  $ year                                                    : int  2012 2012 2012 2012 2012 2012 2012 2012 2012 2012 ...
##  $ EAP2012.Occupation.and.faculty.tenure.status            : Factor w/ 224 levels "","All staff",..: 2 10 7 3 5 11 4 191 199 196 ...
##  $ EAP2012.Total.employees                                 : int  2968 2576 2576 155 2421 332 60 2577 2560 2560 ...
##  $ EAP2012.Institution.employees..excluding.medical.school.: int  2968 2576 2576 155 2421 332 60 2577 2560 2560 ...
##  $ EAP2012.Medical.school.employees                        : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ EAP2012.Full.time.employees                             : int  523 150 150 150 0 315 58 150 150 150 ...
##  $ EAP2012.Full.time.employees..excluding.medical.schools. : int  523 150 150 150 0 315 58 150 150 150 ...
##  $ EAP2012.Full.time.employees..medical.school.            : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ EAP2012.Part.time.employees                             : int  2445 2426 2426 5 2421 17 2 2427 2410 2410 ...
##  $ EAP2012.Part.time.employees..excluding.medical.schools. : int  2445 2426 2426 5 2421 17 2 2427 2410 2410 ...
##  $ EAP2012.Part.time.employees..medical.school.            : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ IDX_HR                                                  : int  -2 -2 -2 -2 -2 -2 -2 -2 -2 -2 ...
```

```r

df10_2 <- read.csv("2012/raw/10_Employees_by_assigned_position_2.csv")
dim(df10_2)
```

```
## [1] 380  31
```

```r
names(df10_2)
```

```
##  [1] "unitid"                                                                                                                                         
##  [2] "institution.name"                                                                                                                               
##  [3] "year"                                                                                                                                           
##  [4] "FLAGS2012.Parent.child.allocation.factor...HR"                                                                                                  
##  [5] "FLAGS2012.Does.institution.have.a.tenure.system"                                                                                                
##  [6] "FLAGS2012.Natural.Disaster.identification"                                                                                                      
##  [7] "FLAGS2012.Response.status.for.EAP"                                                                                                              
##  [8] "FLAGS2012.Response.status.of.institution.for.Human.Resources..HR..component"                                                                    
##  [9] "FLAGS2012.Type.of.Imputation.method...Human.Resources..HR..component"                                                                           
## [10] "FLAGS2012.Status.of.Human.Resources..HR..component.when.data.collection.closed"                                                                 
## [11] "FLAGS2012.Parent.child..indicator...Human.Resources..HR..component"                                                                             
## [12] "FLAGS2012.ID.of.institution.where.data.are.reported.for.the.Human.Resources..HR..component"                                                     
## [13] "DRVHR2012.Total.FTE.staff"                                                                                                                      
## [14] "DRVHR2012.Postsecondary.Teachers.FTE.staff"                                                                                                     
## [15] "DRVHR2012.Postsecondary.Teachers.Instructional.FTE"                                                                                             
## [16] "DRVHR2012.Postsecondary.Teachers.Research.FTE"                                                                                                  
## [17] "DRVHR2012.Postsecondary.Teachers.Public.Service.FTE"                                                                                            
## [18] "DRVHR2012.Librarians..Curators..and.Archivists.and.other.teaching.and.Instructional.support.occupations"                                        
## [19] "DRVHR2012.Librarians..Curators..and.Archivists.FTE"                                                                                             
## [20] "DRVHR2012.Other.teaching.and.Instructional.Support.FTE"                                                                                         
## [21] "DRVHR2012.Management.FTE"                                                                                                                       
## [22] "DRVHR2012.Business.and.Financial.Operations.FTE"                                                                                                
## [23] "DRVHR2012.Computer..Engineering..and.Science.FTE"                                                                                               
## [24] "DRVHR2012.Community.Service..Legal..Arts..and.Media.FTE"                                                                                        
## [25] "DRVHR2012.Healthcare.FTE"                                                                                                                       
## [26] "DRVHR2012.Service..sales..office.admin.support..natural.resources..construction..maintenance..production..transportation...materials.moving.FTE"
## [27] "DRVHR2012.Service.FTE"                                                                                                                          
## [28] "DRVHR2012.Sales.and.Related.FTE"                                                                                                                
## [29] "DRVHR2012.Office.and.Administrative.Support.FTE"                                                                                                
## [30] "DRVHR2012.Natural.Resources..Construction..and.Maintenance.FTE"                                                                                 
## [31] "DRVHR2012.Production..Transportation..and.Material.Moving.FTE"
```

```r
str(df10_2)
```

```
## 'data.frame':	380 obs. of  31 variables:
##  $ unitid                                                                                                                                         : int  125231 142887 143048 143084 143118 143288 143358 144005 144050 144281 ...
##  $ institution.name                                                                                                                               : Factor w/ 378 levels "Adrian College",..: 357 8 265 20 21 32 35 56 299 68 ...
##  $ year                                                                                                                                           : int  2012 2012 2012 2012 2012 2012 2012 2012 2012 2012 ...
##  $ FLAGS2012.Parent.child.allocation.factor...HR                                                                                                  : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ FLAGS2012.Does.institution.have.a.tenure.system                                                                                                : Factor w/ 3 levels "Has tenure system",..: 2 2 1 1 1 1 1 1 1 1 ...
##  $ FLAGS2012.Natural.Disaster.identification                                                                                                      : Factor w/ 1 level "No": 1 1 1 1 1 1 1 1 1 1 ...
##  $ FLAGS2012.Response.status.for.EAP                                                                                                              : Factor w/ 1 level "Respondent": 1 1 1 1 1 1 1 1 1 1 ...
##  $ FLAGS2012.Response.status.of.institution.for.Human.Resources..HR..component                                                                    : Factor w/ 1 level "Respondent": 1 1 1 1 1 1 1 1 1 1 ...
##  $ FLAGS2012.Type.of.Imputation.method...Human.Resources..HR..component                                                                           : Factor w/ 1 level "Not applicable": 1 1 1 1 1 1 1 1 1 1 ...
##  $ FLAGS2012.Status.of.Human.Resources..HR..component.when.data.collection.closed                                                                 : Factor w/ 1 level "Complete, final lock applied": 1 1 1 1 1 1 1 1 1 1 ...
##  $ FLAGS2012.Parent.child..indicator...Human.Resources..HR..component                                                                             : Factor w/ 3 levels "Child record - all data reported with parent campus",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ FLAGS2012.ID.of.institution.where.data.are.reported.for.the.Human.Resources..HR..component                                                     : int  -2 -2 -2 -2 -2 -2 -2 -2 -2 -2 ...
##  $ DRVHR2012.Total.FTE.staff                                                                                                                      : int  1339 70 660 525 507 109 1114 1104 9789 1667 ...
##  $ DRVHR2012.Postsecondary.Teachers.FTE.staff                                                                                                     : int  959 30 317 186 237 47 426 345 3491 875 ...
##  $ DRVHR2012.Postsecondary.Teachers.Instructional.FTE                                                                                             : int  959 30 317 186 237 47 426 345 2132 875 ...
##  $ DRVHR2012.Postsecondary.Teachers.Research.FTE                                                                                                  : int  0 0 0 0 0 0 0 0 1359 0 ...
##  $ DRVHR2012.Postsecondary.Teachers.Public.Service.FTE                                                                                            : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ DRVHR2012.Librarians..Curators..and.Archivists.and.other.teaching.and.Instructional.support.occupations                                        : int  16 1 74 12 9 2 0 22 853 140 ...
##  $ DRVHR2012.Librarians..Curators..and.Archivists.FTE                                                                                             : int  16 1 20 8 9 2 0 22 131 29 ...
##  $ DRVHR2012.Other.teaching.and.Instructional.Support.FTE                                                                                         : int  0 0 54 4 0 0 0 0 722 111 ...
##  $ DRVHR2012.Management.FTE                                                                                                                       : int  228 8 47 51 33 6 58 181 1147 129 ...
##  $ DRVHR2012.Business.and.Financial.Operations.FTE                                                                                                : int  43 0 56 31 20 7 34 56 639 61 ...
##  $ DRVHR2012.Computer..Engineering..and.Science.FTE                                                                                               : int  0 0 36 12 18 4 32 23 1028 83 ...
##  $ DRVHR2012.Community.Service..Legal..Arts..and.Media.FTE                                                                                        : int  34 0 50 40 110 8 1 29 514 139 ...
##  $ DRVHR2012.Healthcare.FTE                                                                                                                       : int  0 0 3 3 5 6 1 51 344 2 ...
##  $ DRVHR2012.Service..sales..office.admin.support..natural.resources..construction..maintenance..production..transportation...materials.moving.FTE: int  59 31 77 190 75 29 562 397 1773 238 ...
##  $ DRVHR2012.Service.FTE                                                                                                                          : int  0 0 5 94 24 3 141 44 379 30 ...
##  $ DRVHR2012.Sales.and.Related.FTE                                                                                                                : int  24 11 1 2 0 10 28 6 19 19 ...
##  $ DRVHR2012.Office.and.Administrative.Support.FTE                                                                                                : int  35 20 71 68 51 12 359 189 1082 189 ...
##  $ DRVHR2012.Natural.Resources..Construction..and.Maintenance.FTE                                                                                 : int  0 0 0 18 0 4 34 127 227 0 ...
##  $ DRVHR2012.Production..Transportation..and.Material.Moving.FTE                                                                                  : int  0 0 0 8 0 0 0 31 66 0 ...
```



