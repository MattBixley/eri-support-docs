# RStudio

## Logging in
![UPDATE WITH PROJECT](../../../assets/images/RStudio_via_OOD_on_NeSI_0.png){width=35%} ![](../../../assets/images/RStudio_via_OOD_on_NeSI_1.png){fig.align="right" width=62%}

## Settings
Recommendation to set *Save Workspace to Never* to avoid saving large files to the workspace. This can be done by going to `Tools` -> `Global Options` -> `General` and setting the `Save workspace to .RData on exit` to `Never`. This will prevent the workspace from being unable to load due to not enough memory in the selected session.

### Plots not showing
The current R modules on OnDemand do not support the default graphics device due to a missing depedency, `cairo`. There is a one off fix for this by changing the backend graphics device from `Default` to `AGG` (Anti-Grain Geometry) in the RStudio settings. 

This can be done by going to `Tools` -> `Global Options` -> `Graphics` and switch `Default` to `AGG`. This will allow the plots to be displayed in the RStudio interface. You do not need to restart the RStudio session for this to take effect.

![](../../../assets/images/RStudio_via_OOD_on_NeSI_2.png)

Modules from 4.4 onwards will have this issue fixed.
