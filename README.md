
# Final Models

This repository provides the final models as supplementary material to the paper 'Sex-specific dimensionless indices for body fat prediction using Continued Fraction Regression'

Additionally, common continued fraction expansions are available in the [Expansions](EXPANSIONS.md)

Please cite as:

```
@misc{Ciezak-2024,
    author      = {Andrew Ciezak and Pablo Moscato},
    title       = {Sex-specific dimensionless indices for body fat prediction using Continued Fraction Regression},
    series      = {},
    year        = {2024},
    pages       = {},
    numpages    = {},
    url         = {},
    doi         = {},
    isbn        = {},
    publisher   = {},
    address     = {},
}
```

# Model Results

These models are output of the paper 'Sex-Specific Dimensionless Indices for Body Fat Prediction: Beyond BMI Using Continued Fraction Regression'.

We define indices $\mathcal{I}(x)$ generated from our employed approach $CFR_{dd}$ that takes as inputs $\mathbf{y}' = CFR_{dd}(\mathbf{y},\mathbf{x},\mathbf{w})$ where
- $\mathbf{y}$ is the 1d array of sample PBF values (target variable)
- $\mathbf{x}$ is the 1d array of sample values for a distance measure
- $\mathbf{w}$ is the 1d array of sample weights for a specific dimensional or dimensionless variable
- $\mathbf{y}$' is the 1d array of sample PBF values (target variable)
- The vectors of $\mathbf{y}', \mathbf{y},\mathbf{x},\mathbf{w}$ have $n$ elements representing values for each of the $n$ samples in the dataset
- The objective function uses the weighted Pearson correlation defined as $R(x, y) = \frac{\sum\limits_{i=1}^{n} w_i (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum\limits_{i=1}^{n} w_i (x_i - \bar{x})^2} \sqrt{\sum\limits_{i=1}^{n} w_i (y_i - \bar{y})^2}}$
- The correlations are based on the training datasets

See the [male]() and [female]() result files for models containing more decimal places.

The primary paper contiains the RMSE scores and classification accuracies in the results section.

## Female Indicies

| Equation | Description | CF  | Depth | Simplified via Mathematica |$R$|
|----------|-----|-----------|---------|-----|----|
| $\mathcal{I}_w\left(x=\dfrac{h}{wa}\right)$  | Index of the most correlated dimensionless variable for the female dataset | $16x+3+\dfrac{15x+2}{x+5+\dfrac{1}{-3x+2+\dfrac{12}{4x+\dfrac{17}{6x-15}}}}$ | 4 | $\dfrac{1152x^5+3408x^4-19920x^3+9050x^2+15899x+2431}{72x^4+132x^3-1065x^2+701x+713}$ | $0.7870$ |
| $\mathcal{I}_w\left(x=\dfrac{ll}{tr}\right)$   | Index of the second most correlated and independent dimensionless variable for the female dataset | $-571+\dfrac{2218x+54}{x+21+\dfrac{293x-148}{-3x-232+\dfrac{1153}{916}}}$ | 3 | $\dfrac{4525956x^2+468554945x-2600401711}{2748x^2+679x+4574107}$ | $0.7335$ |
| $\mathcal{I}_w\left(x=\dfrac{th}{ll}\right)$   | Index of the least correlated dimensionless variable when selecting independent incidies until all base variables appear in a model.   | $-1762+\dfrac{2696}{-x-\frac{-5918x+8383}{2014x}}$  |2 | $\dfrac{5429744x}{2014x^2-5918x+8383}-1762$ | $0.6541$ |
| $BMI$   |  | $\dfrac{we}{h^2}$  | - | - | $0.7822$ |
| $BMI_T$   |  | $\dfrac{we}{h^{2.5}}$  | - | - | $0.7825$ |
| $ABSI$   |  | $\dfrac{wa}{BMI^{\frac{2}{3}}\cdot \sqrt{h}}$  | - | - | $0.1637$ |
| $BRI$   |  | $364.2 - 365.5 \: \sqrt{ 1 - \left( \dfrac{(wa/(2 \: \pi))}{(0.5 \times h)}^2 \right)}$  | - | - | $0.7454$ |

## Female Models

|Desc| Model| $R$| Depth |
|----|-----|------|-----|
|Model from the most corrleated dimensionless index|$\mathcal{M}_{6}\left(x=\mathcal{I}\left(\dfrac{h}{wa}\right)\right)=-0.98x+72.94+\dfrac{8404.05}{-190.53x-\dfrac{5.7}{-9.34+\dfrac{-20.68x+175.91}{-2.75x+39.74}}}$| $0.7874$| 3 |
|Model from the lest correlated dimensionless index| $\mathcal{M}_{7}\left(x=\mathcal{I}\left(\dfrac{th}{ll}\right)\right)=(-0.017x-22.65) $ | $0.6540$ | 0 |
| Model from most and least correlated dimensionless variable| $\mathcal{M}_{8}\left(x_1=\mathcal{I}\left(\dfrac{h}{wa}\right),x_2=\mathcal{I}\left(\dfrac{th}{ll}\right)\right) $</br>$= -1.58x_1-0.0065x_2+\dfrac{93.71x}{0.86x+26.64+\dfrac{-34.55x_2}{3.43x_2+\dfrac{8.12x_2-8.56}{0.67x_1-41.75}}}$ | $0.8072$ | 3 |
| Model from the top two most correlated and independent indices | $\mathcal{M}_{9}\left(x_1=\mathcal{I}\left(\dfrac{h}{wa}\right),x_2=\mathcal{I}\left(\dfrac{ll}{tr}\right)\right) $</br>$= -11.65x_1+0.0033x_2+110.097+\dfrac{-1158025.90x_1-51.79x_2+2706876.79}{233.27x_1-2.60x_2-118524.49}$ | $0.8491$ | 1 |
| Model based on $\mathcal{M}_9$ but including weight and age | $\mathcal{M}_{10}\left(x_1=\mathcal{I}\left(\dfrac{h}{wa}\right),x_2=\mathcal{I}\left(\dfrac{ll}{tr}\right),x_3=we,x_4=ag\right) $</br>$=-0.63x_1-0.0041x_2+0.17x_3+0.12x_4+\dfrac{161.83x_2+780.13x_3+834.77x_4-1750.31}{-23.18x_1+3.27x_2+23.13x_3+23.46x_4}$ | $0.8688$ | 1 |
| Model based on an index from $BMI$ | $\mathcal{M}_{11}\left(x=BMI\right) = 63.56-\dfrac{212.54}{3.11+\dfrac{4.71x}{17.018+\dfrac{109.24}{27.85+\dfrac{-8.89x}{3.58+\dfrac{67.68x}{-30.79x+826.45+\dfrac{17.31}{145.91}}}}}}$ | $0.8118$ | 6 |
| Model based on an index from $BMI_t$ | $\mathcal{M}_{12}\left(x=BMI_T\right) = 53.54-\dfrac{291100.77}{-59.2x+8621.06+\dfrac{-25007576.022x}{-268.21x+19807.81+\dfrac{65200539.26}{-7170x+848.60}}} $ | $0.8116$ | 6 |
| Model based on an index from $ABSI$ | $\mathcal{M}_{13}\left(x=ABSI\right) = 41.21+\dfrac{1.19}{96.93x+\dfrac{-253.15}{52.11+\dfrac{16.31}{12.12x+\dfrac{-40.02}{105.36x+13.46}}}} $ | $0.1883$ |4 |
| Model based on an index from $BRI$ | $\mathcal{M}_{14}\left(x=BRI\right) = 1.08x+36.28+\dfrac{-35.97x-1078.7}{-61.36x+102.33+\dfrac{-885.51x+1.48}{-23.27+\dfrac{-1951.73x}{-22.32x-333.77}}} $ | $0.787$ | 3 |

## Male Indices

| Equation | Description | CF  | Depth | Simplified via Mathematica | $R$|
|----------|-----|-----------|---------|-----|---|
| $\mathcal{I}_m\left(x=\dfrac{h}{wa}\right)$  | Index of the most correlated dimensionless variable for the male dataset | $-59x+25+\dfrac{55x+51}{-63x+179}$ | 1 | $\dfrac{3717x^2-12081x+4526}{179-63x}$ | $0.8537$ |
| $\mathcal{I}_m\left(x=\dfrac{tr}{ll}\right)$   | Index of the second most correlated and independent dimensionless variable for the male dataset  | $-21x+17+\dfrac{13x-57}{-x-21+\dfrac{-21x+30}{-30x+1-\dfrac{1}{23x}}}$ | 3 | $-\dfrac{14490x^4+290904x^3-272989x^2-1771x-414}{690x^3+13984x^2+208x+21}$ | $0.7795$ |
| $\mathcal{I}_m\left(x=\dfrac{ll}{ss}\right)$   | Index of the least correlated dimensionless variable when selecting independent incidies until all base variables appear in a model. | $-161+\dfrac{-120x-60}{-11-\dfrac{187}{-1+\dfrac{435}{x+221}}}$ | 3 | $-\dfrac{120x^2+2716x+7019801}{176x+43681}$ | $0.7182$ |
| $BMI$   |  | $\dfrac{we}{h^2}$  | - | | $0.7224$ |
| $BMI_T$   |  | $\dfrac{we}{h^{2.5}}$  | - |  | $0.7233$ |
| $ABSI$   |  | $\dfrac{wa}{BMI^{\frac{2}{3}}\cdot \sqrt{h}}$  | - |  | $0.5504$ |
| $BRI$   |  | $364.2 - 365.5 \: \sqrt{ 1 - \left( \dfrac{(wa/(2 \: \pi))}{(0.5 \times h)}^2 \right)}$  | - |  | $0.8309$ |

## Male Models

|Desc| Model| $R$| Depth |
|----|-----|------|------|
|Model from the most corrleated dimensionless index|$\mathcal{M}_{6}\left(x=\mathcal{I}\left(\dfrac{h}{wa}\right)\right)=0.3749x+57.56$| $0.8537$ | 0 |
|Model from the lest correlated dimensionless index| $\mathcal{M}_{7}\left(x=\mathcal{I}\left(\dfrac{ll}{ss}\right)\right)=-1.12x-139.32$ | $0.7182$ | 0 |
| Model from most and least correlated dimensionless variable| $\mathcal{M}_{8}\left(x_1=\mathcal{I}\left(\dfrac{h}{wa}\right),x_2=\mathcal{I}\left(\dfrac{ll}{ss}\right)\right) = 65.088+\dfrac{297918.24}{17.20x_2+11.45+\dfrac{-50174.42x_2-758722.39}{15.67x_1}}$ | $0.8624$ | 2 |
| Model from the top two most correlated and independent indices | $\mathcal{M}_{9}\left(x_1=\mathcal{I}\left(\dfrac{h}{wa}\right),x_2=\mathcal{I}\left(\dfrac{ll}{tr}\right)\right) $</br>$= -11.65x_1+0.0033x_2+110.097+\dfrac{-1158025.90x_1-51.79x_2+2706876.79}{233.27x_1-2.60x_2-118524.49}$ | $0.867$ | 1 |
| Model based on $\mathcal{M}_9$ but including weight and age | $\mathcal{M}_{10}\left(x_1=\mathcal{I}\left(\dfrac{h}{wa}\right),x_2=\mathcal{I}\left(\dfrac{tr}{ll}\right),x_3=we,x_4=ag\right) $<br>$=-0.3x_1-7.77x_2-0.27x_3+0.65x_4+154.18+\dfrac{26.89x_1+90.73x_2+14.67x_3-31.67x_4-236.25}{1.14x_2+29.06+\dfrac{3405039.97x_2+2463772.87x_4+8.40}{1800356.74x_3+2204326.56+\dfrac{16469628.13x_1+103290.61x_3-2694017.59}{-2951139.64x_2-3023352.08x_3-1824579.97x_4-695708.71}}}$ | $0.9$ | 3 |
| Model based on $BMI$ | $\mathcal{M}_{11}\left(x=BMI\right) = 56.16+\dfrac{1.04}{-0.0017+0.02+\dfrac{2.79}{-9.68x+\dfrac{-23.744x}{-5.62+\dfrac{13.084x}{22.067}}}} $ | $0.7206$ | 4 |
| Model based on $BMI_T$| $\mathcal{M}_{12}\left(x=BMI_t\right) = -8.023*x+28.53+\dfrac{114.96x-488.64}{0.028x+11.35}$ | $0.7265$ | 1 |
| Model based on $ABSI$ | $\mathcal{M}_{13}\left(x=ABSI\right) = 1996.34x-53.93+\dfrac{-113.43x-1622.0253}{-311.40x+45.39}$ | $0.5634$ | 1 |
| Model based on $BRI$ | $\mathcal{M}_{14}\left(x=BRI\right) = 89.36+\dfrac{-31.88x-122.45}{0.84x+\dfrac{5.48}{3.40+\dfrac{39.37x}{29.18}}} $ | $0.8531$ | 3 |
