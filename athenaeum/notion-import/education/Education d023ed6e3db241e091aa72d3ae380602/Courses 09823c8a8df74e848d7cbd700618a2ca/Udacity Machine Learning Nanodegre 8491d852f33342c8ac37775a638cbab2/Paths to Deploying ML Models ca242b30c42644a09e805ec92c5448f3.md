# Paths to Deploying ML Models

### **Paths to Deployment**

There are *three* primary methods used to transfer a model from the ***modeling*** *component* to the ***deployment*** *component* of the machine learning workflow. We will be discussing them in *order* of ***least*** to ***most*** commonly used. The ***third*** *method* that's *most* similar to what’s used for *deployment* within ***Amazon’s SageMaker***.

### **Paths to *Deployment*:**

1. Python model is *recoded* into the programming language of the production environment.
2. Model is *coded* in *Predictive Model Markup Language* (PMML) or *Portable Format Analytics* (PFA).
3. Python model is *converted* into a format that can be used in the production environment.

### **Recoding Model into Programming Language of Production Environment**

The *first* method which involves recoding the Python model into the language of the production environment, often Java or C++. This method is *rarely used anymore* because it takes time to recode, test, and validate the model that provides the *same* predictions as the *original*.

### **Model is Coded in PMML or PFA**

The *second* method is to code the model in Predictive Model Markup Language (PMML) or Portable Format for Analytics (PFA), which are two complementary standards that *simplify* moving predictive models to *deployment* into a *production environment*. The Data Mining Group developed both PMML and PFA to provide vendor-neutral executable model specifications for certain predictive models used by data mining and machine learning. Certain analytic software allows for the direct import of PMML including but *not limited* to IBM SPSS, R, SAS Base & Enterprise Miner, Apache Spark, Teradata Warehouse Miner, and TIBCO Spotfire.

### **Model is Converted into Format that’s used in the Production Environment**

The *third* method is to build a Python model and ***use*** *libraries* and *methods* that *convert* the model into ***code*** that can be used in the *production environment*. Specifically *most* popular machine learning software frameworks, like PyTorch, TensorFlow, SciKit-Learn, have methods that will *convert* Python models into *intermediate standard format*, like ONNX (**[Open Neural Network Exchange](https://onnx.ai/)** format). This *intermediate standard format* then can be ***converted*** into the software native to the *production environment*.

- This is the *easiest* and *fastest* way ***to move*** a Python model from *modeling* directly to *deployment*.
- Moving forward this is *typically* the way *models* are ***moved*** into the *production environment*.
- Technologies like *containers*, *endpoints*, and *APIs* (Application Programming Interfaces) also help ***ease*** the ***work*** required for *deploying* a model into the *production environment*.