---
layout: default
---

## 电催化微观动力学建模

### ORR反应过程

1. 第一步氧气扩散到催化剂附近的双电层:  
<img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}(\mathrm{aq})&space;\underset{k_{-1}}{\stackrel{k_{1}}{\rightleftharpoons}}&space;\mathrm{O}_{2}(\mathrm{dl})" title="\mathrm{O}_{2}(\mathrm{aq}) \underset{k_{-1}}{\stackrel{k_{1}}{\rightleftharpoons}} \mathrm{O}_{2}(\mathrm{dl})" />
2. 第二步氧气吸附  
<img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}(\mathrm{dl})&plus;*_{\mathrm{A}}&space;\underset{k_{-2}}{\stackrel{k_{2}}{\rightleftharpoons}}&space;\mathrm{O}_{2}&space;*_{\mathrm{A}}" title="\mathrm{O}_{2}(\mathrm{dl})+*_{\mathrm{A}} \underset{k_{-2}}{\stackrel{k_{2}}{\rightleftharpoons}} \mathrm{O}_{2} *_{\mathrm{A}}" />
3. 第三步\*OOH  
<img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-3}}{\stackrel{k_{3}}{\rightleftharpoons}}&space;\mathrm{OOH}&space;*_{\mathrm{A}}" title="\mathrm{O}_{2} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-3}}{\stackrel{k_{3}}{\rightleftharpoons}} \mathrm{OOH} *_{\mathrm{A}}" />
4. 第四步\*O  
<img src="https://latex.codecogs.com/svg.image?\mathrm{OOH}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-4}}{\stackrel{k_{4}}{\rightleftharpoons}}&space;\mathrm{O}&space;*_{\mathrm{A}}&plus;\mathrm{H}_{2}&space;\mathrm{O}" title="\mathrm{OOH} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-4}}{\stackrel{k_{4}}{\rightleftharpoons}} \mathrm{O} *_{\mathrm{A}}+\mathrm{H}_{2} \mathrm{O}" />
5. 第五步\*OH  
<img src="https://latex.codecogs.com/svg.image?\mathrm{O}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-5}}{\stackrel{k_{5}}{\rightleftharpoons}}&space;\mathrm{OH}&space;*_{\mathrm{A}}" title="\mathrm{O} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-5}}{\stackrel{k_{5}}{\rightleftharpoons}} \mathrm{OH} *_{\mathrm{A}}" />
6. 第六步H2O  
<img src="https://latex.codecogs.com/svg.image?\mathrm{OH}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-6}}{\stackrel{k_{6}}{\rightleftharpoons}}&space;*_{\mathrm{A}}&plus;\mathrm{H}_{2}&space;\mathrm{O}" title="\mathrm{OH} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-6}}{\stackrel{k_{6}}{\rightleftharpoons}} *_{\mathrm{A}}+\mathrm{H}_{2} \mathrm{O}" />

建立微分方程
1. 双电层中的氧气  
<img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;x_{\mathrm{O}_{2}(\mathrm{dl})}}{\partial&space;t}=k_{1}&space;x_{\mathrm{O}_{2}(\mathrm{aq})}-k_{-1}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}-k_{2}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}&space;\theta_{*_{\mathrm{A}}}&plus;k_{-2}&space;\theta_{\mathrm{O}_{2}&space;*&space;\mathrm{~A}}" title="\frac{\partial x_{\mathrm{O}_{2}(\mathrm{dl})}}{\partial t}=k_{1} x_{\mathrm{O}_{2}(\mathrm{aq})}-k_{-1} x_{\mathrm{O}_{2}(\mathrm{dl})}-k_{2} x_{\mathrm{O}_{2}(\mathrm{dl})} \theta_{*_{\mathrm{A}}}+k_{-2} \theta_{\mathrm{O}_{2} * \mathrm{~A}}" />
2. 位点A  
<img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{*_{\mathrm{A}}}}{\partial&space;t}=k_{6}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}-k_{-6}&space;\theta_{*_{\mathrm{A}}}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}-k_{2}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}&space;\theta_{*_{\mathrm{A}}}&plus;k_{-2}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}" title="\frac{\partial \theta_{*_{\mathrm{A}}}}{\partial t}=k_{6} \theta_{\mathrm{OH} *_{\mathrm{A}}}-k_{-6} \theta_{*_{\mathrm{A}}} x_{\mathrm{H}_{2} \mathrm{O}}-k_{2} x_{\mathrm{O}_{2}(\mathrm{dl})} \theta_{*_{\mathrm{A}}}+k_{-2} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}}" />
3. 位点A吸附氧气  
<img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{O}_{2}&space;*&space;\mathrm{~A}}}{\partial&space;t}=k_{2}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}&space;\theta_{*_{\mathrm{A}}}-k_{-2}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}-k_{3}&space;\theta_{\mathrm{O}_{2}&space;*&space;\mathrm{~A}}&plus;k_{-3}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}" title="\frac{\partial \theta_{\mathrm{O}_{2} * \mathrm{~A}}}{\partial t}=k_{2} x_{\mathrm{O}_{2}(\mathrm{dl})} \theta_{*_{\mathrm{A}}}-k_{-2} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}}-k_{3} \theta_{\mathrm{O}_{2} * \mathrm{~A}}+k_{-3} \theta_{\mathrm{OOH} *_{\mathrm{A}}}" />
4. 位点A吸附OOH  
<img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}}{\partial&space;t}=k_{3}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}-k_{-3}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}-k_{4}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}&plus;k_{-4}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}" title="\frac{\partial \theta_{\mathrm{OOH} *_{\mathrm{A}}}}{\partial t}=k_{3} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}}-k_{-3} \theta_{\mathrm{OOH} *_{\mathrm{A}}}-k_{4} \theta_{\mathrm{OOH} *_{\mathrm{A}}}+k_{-4} x_{\mathrm{H}_{2} \mathrm{O}} \theta_{\mathrm{O} *_{\mathrm{A}}}" />
5. 位点A吸附O  
<img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}}{\partial&space;t}=k_{4}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}-k_{-4}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}-k_{5}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}&plus;k_{-5}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}" title="\frac{\partial \theta_{\mathrm{O} *_{\mathrm{A}}}}{\partial t}=k_{4} \theta_{\mathrm{OOH} *_{\mathrm{A}}}-k_{-4} x_{\mathrm{H}_{2} \mathrm{O}} \theta_{\mathrm{O} *_{\mathrm{A}}}-k_{5} \theta_{\mathrm{O} *_{\mathrm{A}}}+k_{-5} \theta_{\mathrm{OH} *_{\mathrm{A}}}" />
6. 位点A吸附OH  
<img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}}{\partial&space;t}=k_{5}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}-k_{-5}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}-k_{6}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}&plus;k_{-6}&space;\theta_{*_{\mathrm{A}}}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}" title="\frac{\partial \theta_{\mathrm{OH} *_{\mathrm{A}}}}{\partial t}=k_{5} \theta_{\mathrm{O} *_{\mathrm{A}}}-k_{-5} \theta_{\mathrm{OH} *_{\mathrm{A}}}-k_{6} \theta_{\mathrm{OH} *_{\mathrm{A}}}+k_{-6} \theta_{*_{\mathrm{A}}} x_{\mathrm{H}_{2} \mathrm{O}}" />

位点守恒  
<img src="https://latex.codecogs.com/svg.image?1=\theta_{*_{\mathrm{A}}}&plus;\theta_{\mathrm{O}_{2}&space;*&space;\mathrm{~A}}&plus;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}&plus;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}&plus;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}" title="1=\theta_{*_{\mathrm{A}}}+\theta_{\mathrm{O}_{2} * \mathrm{~A}}+\theta_{\mathrm{OOH} *_{\mathrm{A}}}+\theta_{\mathrm{O} *_{\mathrm{A}}}+\theta_{\mathrm{OH} *_{\mathrm{A}}}" />




[[Back]](../)
