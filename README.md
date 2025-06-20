# Optical System Camera Coupling Calculator

## Mathematical Formulas

This document describes all the mathematical formulas implemented in the optical system camera coupling calculator using proper mathematical notation.

### 1. Magnification Calculations

#### Total Magnification
$M_{total} = M_{obj} \times M_{corr}$

where:
- $M_{total}$ = Total system magnification
- $M_{obj}$ = Objective lens magnification
- $M_{corr}$ = Magnification correction factor

#### Magnification Correction (for extension tubes)
$M_{corr} = \begin{cases} 
\frac{f_{tube}}{d_{eff}} & \text{if } d_{eff} > 180\text{mm} \\
1.0 & \text{otherwise}
\end{cases}$

$d_{eff} = d_{flange} + d_{ext}$

where:
- $f_{tube}$ = Tube lens focal length (mm)
- $d_{eff}$ = Effective back focus distance (mm)
- $d_{flange}$ = Mount flange distance (mm)
- $d_{ext}$ = Extension tube length (mm)

### 2. Field of View

#### Field of View at Object Plane
$FOV = \frac{FN}{M_{total}}$

where:
- $FOV$ = Field of view at object plane (mm)
- $FN$ = Field number of objective lens (mm)

### 3. Resolution Calculations

#### Spatial Resolution (Diffraction Limited)
$R_{spatial} = \frac{0.61 \lambda}{NA}$

where:
- $R_{spatial}$ = Spatial resolution limit (μm)
- $\lambda$ = Wavelength (μm)
- $NA$ = Numerical aperture of objective lens

#### Pixel Resolution at Object Plane
$R_{pixel} = \frac{p}{M_{total}}$

where:
- $R_{pixel}$ = Pixel resolution at object plane (μm)
- $p$ = Camera pixel size (μm)

#### Nyquist Criterion
$\text{Nyquist satisfied} = R_{pixel} \leq \frac{R_{spatial}}{2}$

### 4. Light Collection Efficiency

#### Tube Lens Numerical Aperture
$NA_{tube} = \frac{D_{tube}}{2f_{tube}}$

where:
- $NA_{tube}$ = Tube lens numerical aperture
- $D_{tube}$ = Tube lens diameter (mm)

#### Light Collection Efficiency
$\eta_{light} = \min\left(100\%, \left(\frac{NA_{obj}}{NA_{tube}}\right)^2 \times 100\%\right)$

where:
- $\eta_{light}$ = Light collection efficiency (%)
- $NA_{obj}$ = Objective lens numerical aperture

### 5. System Transmission

#### Overall System Transmission
$T_{system} = T_{tube} \times QE_{camera}$

where:
- $T_{system}$ = Total system transmission
- $T_{tube}$ = Tube lens transmission (0-1)
- $QE_{camera}$ = Camera quantum efficiency (0-1)

### 6. Vignetting Analysis

#### Sensor Diagonal
$d_{sensor} = \sqrt{w_{sensor}^2 + h_{sensor}^2}$

where:
- $d_{sensor}$ = Sensor diagonal (mm)
- $w_{sensor}$ = Sensor width (mm)
- $h_{sensor}$ = Sensor height (mm)

#### Tube Image Circle
$D_{image} = \min(0.8 \times D_{tube}, 0.9 \times D_{mount})$

where:
- $D_{image}$ = Effective image circle diameter (mm)
- $D_{mount}$ = Mount aperture diameter (mm)

#### Image Circle Coverage
$C_{coverage} = \min\left(100\%, \frac{D_{image}}{d_{sensor}} \times 100\%\right)$

#### Maximum Field Angle
$\theta_{max} = \arctan\left(\frac{d_{sensor}}{2f_{tube}}\right) \times \frac{180°}{\pi}$

where:
- $\theta_{max}$ = Maximum field angle (degrees)

#### Mount Vignetting Factor
$V_{mount} = \min\left(1, \frac{D_{mount}}{1.2 \times d_{sensor}}\right)$

#### Corner Illumination (Cos⁴ Law)
$I_{corner} = \cos^4(\theta_{max}) \times V_{mount} \times 100\%$

where:
- $I_{corner}$ = Corner illumination (%)

#### Vignetting Level Classification
$\text{Vignetting Level} = \begin{cases}
\text{Severe} & \text{if } C_{coverage} < 90\% \\
\text{Moderate} & \text{if } I_{corner} < 70\% \\
\text{Mild} & \text{if } I_{corner} < 85\% \\
\text{None} & \text{otherwise}
\end{cases}$

### 7. Mount Specifications

| Mount Type | Flange Distance $d_{flange}$ (mm) | Aperture Diameter $D_{mount}$ (mm) |
|------------|-----------------------------------|-------------------------------------|
| C-mount    | 17.526                           | 23.1                                |
| CS-mount   | 12.5                             | 23.1                                |
| F-mount    | 46.5                             | 41.0                                |
| T-mount    | 55.0                             | 38.1                                |
| M42        | 45.5                             | 38.1                                |

## Performance Criteria

### Resolution Matching
- **Undersampling**: $R_{pixel} > \frac{R_{spatial}}{2}$
- **Optimal sampling**: $\frac{R_{spatial}}{3} \leq R_{pixel} \leq \frac{R_{spatial}}{2}$
- **Oversampling**: $R_{pixel} < \frac{R_{spatial}}{3}$

### Light Collection Efficiency
- **Poor**: $\eta_{light} < 50\%$
- **Moderate**: $50\% \leq \eta_{light} < 70\%$
- **Good**: $\eta_{light} \geq 70\%$

### Vignetting Assessment
- **None**: $I_{corner} > 85\%$ and $C_{coverage} > 90\%$
- **Mild**: $70\% \leq I_{corner} \leq 85\%$
- **Moderate**: $I_{corner} < 70\%$
- **Severe**: $C_{coverage} < 90\%$

## Key Constants

- **Diffraction constant**: 0.61 (Rayleigh criterion)
- **Default wavelength**: $\lambda = 550$ nm (green light)
- **Image circle efficiency**: 0.8 (80% of tube lens diameter)
- **Mount efficiency**: 0.9 (90% of mount aperture)

## References

1. Born, M. & Wolf, E. *Principles of Optics* - Diffraction theory
2. Hecht, E. *Optics* - Geometric optics and imaging systems
3. ISO standards for microscope mount specifications
4. Photographic lens design principles for vignetting calculations
