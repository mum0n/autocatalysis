### Network theory

How is a system organised. How inter-related or linked is the system. Does this have an influence upon it's structural and dynamical characterstics? Does it influence the stability of a system?
This has been a core area of study that has waxed and waned over the years but never without any real resolution.
MacArthur clearly expressed this question in a classic paper. Others have studied the problem numerically (i.e., May, Ashby, etc.). 

Current approaches are many: Patten, Ulanowicz, Oster. And many recent studies of Self-organised critical systems and small world networks are striking and deeply resonant with the stability characteristics of the most general networks.
Topology does influence the critical (synchronous) behaviour of complex middle number systems.
 

### Linear Network Analysis

Here is an R/Splus language implementation of the linear network analytical methods
[(they are called R/NEA*)](https://github.com/mum0n/ecomod) originally published by Brian D. Fath and Stuart R. Borrett (2004) in MATLAB (NEA.m, version 1.0.0).
 
An example of usage is demonstrated: 

```
# parameters
#
# The input variable 'data' is an (n+1 x n+2) matrix composed of:
#
# F = flow matrix [nxn]
# z = input vector [nx1]
# x = storage vector [nx1]
# y = output vector [1xn]
# .. a 1x2 vector of zeros. 
#
# Sample data from the intertidal oyster reef ecosystem model created by Dame and Patten (1981)
# From Patten (1985).  Model flows are in kcal m^-2 day^-1;
# storage data is kcal m^-2.
# Dame, R. F., and B. C. Patten. 1981. Analysis of energy flows in an
# intertidal oyster reef. Marine Ecology Progress Series 5:115-124.
# Patten, B. C. 1985. Energy cycling, length of food chains, and direct
# versus indirect effects in ecosystems. Can. Bull. Fish. Aqu. Sci. 213:119-138.
# Network Environ Analysis
source(file.path("http://sites.google.com/site/autocatalysis/NEA.functions.r"))
# labels
Compartments = c( "Filter Feeders", "Deposited Detritus", "Microbiota",
                  "Meiofauna", "Deposit Feeders", "Predators")
# Steady-State Flow Matrix
F = matrix( c(0, 0, 0, 0, 0, 0,
              15.7915, 0, 0, 4.2403, 1.9076, 0.3262,
              0, 8.1721, 0, 0, 0, 0,
              0, 7.2745, 1.2060, 0, 0, 0,
              0, 0.6431, 1.2060, 0.6609, 0, 0,
              0.5135, 0, 0, 0, 0.1721, 0),
            nrow=length(Compartments), byrow=T, dimnames=list(Compartments,Compartments)  )
# Steady-State Storage Vector
x = c(2000, 1000, 2.4121, 24.121, 16.274, 69.237)   
# Steady-state Input Vector
z = c(41.4697, 0, 0, 0, 0, 0)
# Steady-State Outputs
y = c(25.1646, 6.1759, 5.7600, 3.5794, 0.4303, 0.3594)
# Ensure steady-state
  check.data( F,z )
# Structural Analysis
  SAnal = NEA_structure(F)
  SAnal
# Throughflow Analysis
  TFAnal = NEA_throughflow(F,y,z)
  TFAnal
# Storage Analysis
  StAnal = NEA_storage(F,x)
  StAnal
 
# Utility Analysis
  UtAnal = NEA_utility(F,x)
  UtAnal
# Unit Environ Analysis
  Unit.Environs = NEA_u_environs(TFAnal, StAnal)
  Unit.Environs
# Control Analysis
  CtrlAnal = NEA_control( TFAnal, StAnal )
  CtrlAnal
```

### Source

Fath, B.D. & Borrett, S.R. 2004. A MATLAB function for Network Environ Analysis. Environmental Modelling and Software 21:375-405.


