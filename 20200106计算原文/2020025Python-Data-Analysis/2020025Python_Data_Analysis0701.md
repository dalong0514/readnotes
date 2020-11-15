# 07 Signal Processing and Time Series

Signal processing is a field of engineering and applied mathematics that analyzes analog and digital signals, corresponding to variables that vary with time. One of the categories of signal processing techniques is time series analysis. A time series is an ordered list of data points starting with the oldest measurements first. The data points are usually equidistant, for instance, consistent with daily or annual sampling. In time series analysis, the order of the values is important. It's common to try to derive a relation between a value and another data point or combination of data points a fixed number of periods in the past, in the same time series.

The time series examples in this chapter use annual sunspot cycles data. This data is provided by the statsmodels package (an open source Python project). The examples use NumPy/SciPy, pandas, and also statsmodels.

## 01. statsmodels subpackages

To install statsmodels, execute the following command:

```
$ pip install statsmodels 
$ pip freeze|grep stat statsmodels==0.6.0
```

Open the pkg_check.py file provided in the code bundle, and change the code to list the statsmodels subpackages to get the following result:

## 02. Moving averages

Moving averages are frequently used to analyze time series. A moving average specifies a window of data that is previously seen, which is averaged each time the window slides forward by one period:

The different types of moving averages differ essentially in the weights used for averaging. The exponential moving average, for instance, has exponentially decreasing weights with time:

This means that older values have less influence than newer values, which is sometimes desirable.

The following code from the moving_average.py file in this book's code bundle plots the simple moving average for the 11- and 22-year sunspots cycles:

```
import matplotlib.pyplot as plt 
import statsmodels.api as sm 
# from pandas.stats.moments import rolling_mean「rolling_mean has been removed in the new version」
import pandas as pd 

data_loader = sm.datasets.sunspots.load_pandas()
df = data_loader.data 
year_range = df["YEAR"].values

plt.plot(year_range, df["SUNACTIVITY"].values, label="Original")
# plt.plot(year_range, pd.rolling_mean(df, 11)["SUNACTIVITY"].values, label="SMA 11")「the style of old version」
plt.plot(year_range, df.rolling(window=11,center=False).mean()["SUNACTIVITY"].values, label="SMA 11")
plt.plot(year_range, df.rolling(window=22,center=False).mean()["SUNACTIVITY"].values, label="SMA 22")
plt.legend()
plt.show()
```

We can express an exponential decreasing weight strategy for the exponential moving average, as shown in the following NumPy code:

```
weights = np.exp(np.linspace(-1., 0., N))
weights /= weights.sum()
```

A simple moving average uses equal weights, which in code looks as follows:

```
def sma(arr, n):
    weights = np.ones(n) / n
    return np.convolve(weights, arr)[n-1:-n+1]
```

Since we can load the data into a pandas DataFrame, it is more convenient to use the pandas rolling_mean() function. Load the data as follows using statsmodels:

```
data_loader = sm.datasets.sunspots.load_pandas() 
df = data_loader.data
```

Refer to the following plot for the end result:

## 03. Window functions

NumPy has a number of window routines that can compute weights in a rolling window as we did in the previous section.






A window function is a function that is defined within an interval (the window) or is otherwise zero valued. We can use window functions for spectral analysis and filter design (for more background information, refer to http://en.wikipedia.org/ wiki/Window_function). The boxcar window is a rectangular window with the following formula:

w(n) = 1

[ 168 ] Chapter 7

The triangular window is shaped like a triangle and has the following formula:

N −1 nw ( n ) = 1− | L 2 | 2

In the preceding formula, L can be equal to N, N+1, or N-1. In the last case, the window function is called the Bartlett window. The Blackman window is bell shaped and defined as follows:

 2π n   4π n  ( ) w n = a 0 − a 1   + a2 cos cos    N −1   N −1 

1−α 1 α a 0 = ;a 1 = ;a 2 = 2 2 2

The Hanning window is also bell shaped and defined as follows:

 2π  n w ( n ) = 0.5  1 − cos        N −1  

In the pandas API, the rolling_window() function provides the same functionality with different values of the win_type string parameter corresponding to different window functions. The other parameter is the size of the window, which will be set to 22 for the middle cycle of the sunspots data (according to research, there are three cycles of 11, 22, and 100 years). The code is straightforward and given in the window_functions.py file in this book's code bundle (the data here is limited to the last 150 years only for easier comparison in the plots):

import matplotlib.pyplot as plt import statsmodels.api as sm from pandas.stats.moments import rolling_window import pandas as pd

data_loader = sm.datasets.sunspots.load_pandas() df = data_loader.data.tail(150)

df = pd.DataFrame({'SUNACTIVITY':df['SUNACTIVITY'].values},

index=df['YEAR']) ax = df.plot()

def plot_window(win_type):

df2 = rolling_window(df, 22, win_type)

[ 169 ] Signal Processing and Time Series

df2.columns = [win_type] df2.plot(ax=ax)

plot_window('boxcar') plot_window('triang') plot_window('blackman') plot_window('hanning') plot_window('bartlett') plt.show()

Refer to the following plot for the end result:

## 04. Defining cointegration

Cointegration is similar to correlation but is viewed by many as a superior metric to define the relatedness of two time series. Two time series x(t) and y(t) are cointegrated if a linear combination of them is stationary. In such a case, the following equation should be stationary:

y(t) – a x(t)

[ 170 ] Chapter 7

Consider a drunk man and his dog out on a walk. Correlation tells us whether they are going in the same direction. Cointegration tells us something about the distance over time between the man and his dog. We will show cointegration using randomly generated time series and real data. The Augmented Dickey-Fuller (ADF) test (see http://en.wikipedia.org/wiki/Augmented_Dickey%E2%80%93Fuller_test) tests for a unit root in a time series and can be used to determine the cointegration of time series.

For the following code, have a look at the cointegration.py file in this book's code bundle:

import statsmodels.api as sm from pandas.stats.moments import rolling_window import pandas as pd import statsmodels.tsa.stattools as ts import numpy as np

def calc_adf(x, y):

result = sm.OLS(x, y).fit() return ts.adfuller(result.resid)

data_loader = sm.datasets.sunspots.load_pandas() data = data_loader.data.values N = len(data)

t = np.linspace(-2 * np.pi, 2 * np.pi, N) sine = np.sin(np.sin(t)) print "Self ADF", calc_adf(sine, sine)

noise = np.random.normal(0, .01, N) print "ADF sine with noise", calc_adf(sine, sine + noise)

cosine = 100 * np.cos(t) + 10 print "ADF sine vs cosine with noise", calc_adf(sine, cosine + noise)

print "Sine vs sunspots", calc_adf(sine, data)

Let's get started with the cointegration demo:

1. Define the following function to calculate the ADF statistic:

def calc_adf(x, y):

result = stat.OLS(x, y).fit() return ts.adfuller(result.resid)

[ 171 ] Signal Processing and Time Series

2. Load the sunspots data into a NumPy array:

data_loader = sm.datasets.sunspots.load_pandas() data = data_loader.data.values N = len(data)

3. Generate a sine and calculate the cointegration of the sine with itself:

t = np.linspace(-2 * np.pi, 2 * np.pi, N) sine = np.sin(np.sin(t)) print "Self ADF", calc_adf(sine, sine)

The code should print the following:

Self ADF (-5.0383000037165746e-16, 0.95853208606005591, 0, 308, {'5%': -2.8709700936076912, '1%': -3.4517611601803702, '10%': -2.5717944160060719}, -21533.113655477719)

The first value in the printout is the ADF metric and the second value is the p-value. As you can see, the p-value is very high. The following values are the lag and sample size. The dictionary at the end gives the t-distribution values for this exact sample size.

4. Now, add noise to the sine to demonstrate how noise will influence the signal:

noise = np.random.normal(0, .01, N) print "ADF sine with noise", calc_adf(sine, sine + noise)

With the noise, we get the following results:

ADF sine with noise (-7.4535502402193075, 5.5885761455106898e-11, 3, 305, {'5%': -2.8710633193086648, '1%': -3.4519735736206991, '10%': -2.5718441306100512}, 1855.0243977703672)

The p-value has gone down considerably. The ADF metric -7.45 here is lower than all the critical values in the dictionary. All these are strong arguments to reject cointegration.

5. Let's generate a cosine of a larger magnitude and offset. Again, let's add noise to it:

cosine = 100 * np.cos(t) + 10 print "ADF sine vs cosine with noise", calc_adf(sine, cosine + noise)

The following values get printed:

ADF sine vs cosine with noise (-17.927224617871534, 2.8918612252729532e-30, 16, 292, {'5%': -2.8714895534256861, '1%': -3.4529449243622383, '10%': -2.5720714378870331}, 11017.837238220782)

[ 172 ] Chapter 7

Similarly, we have strong arguments to reject cointegration. Checking for cointegration between the sine and sunspots gives the following output:

Sine vs sunspots (-6.7242691810701016, 3.4210811915549028e-09, 16, 292, {'5%': -2.8714895534256861, '1%': -3.4529449243622383, '10%': 2.5720714378870331}, -1102.5867415291168)

The confidence levels are roughly the same for the pairs used here because they are dependent on the number of data points, which don't vary much. The outcome is summarized in the following table:

## 05. Autocorrelation

Autocorrelation is correlation within a dataset and can indicate a trend.

For a given time series, with known mean and standard deviations, we can define the autocorrelation for times s and t using the expected value operator as follows:

E   ( x t − µ t )( x s − µ s )   σt σs 

This is, in essence, the formula for correlation applied to a time series and the same time series lagged.

For example, if we have a lag of one period, we can check if the previous value influences the current value. For that to be true, the autocorrelation value has to be pretty high.

[ 173 ] Signal Processing and Time Series

In the previous chapter, Chapter 6, Data Visualization, we already used a pandas function that plots autocorrelation. In this example, we will use the NumPy correlate() function to calculate the actual autocorrelation values for the sunspots cycle. At the end, we need to normalize the values we receive.

Apply the NumPy correlate() function as follows:

y = data - np.mean(data) norm = np.sum(y ** 2) correlated = np.correlate(y, y, mode='full')/norm

We are also interested in the indices corresponding to the highest correlations. These indices can be found with the NumPy argsort() function, which returns the indices that would sort an array:

print np.argsort(res)[-5:]

These are the indices found for the largest autocorrelations:

[ 9 11 10

1

0]

The largest autocorrelation is by definition for zero lag, that is, the correlation of a signal with itself. The next largest values are for a lag of one and ten years. Check the autocorrelation.py file in this book's code bundle:

import numpy as np import pandas as pd import statsmodels.api as sm import matplotlib.pyplot as plt from pandas.tools.plotting import autocorrelation_plot

data_loader = sm.datasets.sunspots.load_pandas() data = data_loader.data["SUNACTIVITY"].values y = data - np.mean(data) norm = np.sum(y ** 2) correlated = np.correlate(y, y, mode='full')/norm res = correlated[len(correlated)/2:]

print np.argsort(res)[-5:] plt.plot(res) plt.grid(True) plt.xlabel("Lag") plt.ylabel("Autocorrelation") plt.show() autocorrelation_plot(data) plt.show()

[ 174 ] Chapter 7

Refer to the following plot for the end result:

Compare the previous plot with the plot produced by pandas:

[ 175 ] Signal Processing and Time Series

## 06. Autoregressive models

An autoregressive model can be used to represent a time series with the goal of forecasting future values. In such a model, a variable is assumed to depend on its previous values. The relation is also assumed to be linear and we are required to fit the data in order to find the parameters of the data.

The mathematical formula for the autoregressive model is as follows:

p x t = c + ∑ a i x t − i +∈t  i =1

In the preceding formula, c is a constant and the last term is a random component also known as white noise.

This presents us with the very common problem of linear regression. For practical reasons, it's important to keep the model simple and only involve necessary lagged components. In machine learning jargon, these are called features. For regression problems, the Python machine learning scikit-learn library is a good, if not the best, choice. We will work with this API in Chapter 10, Predictive Analytics and Machine Learning.

In regression setups, we frequently encounter the problem of overfitting—this issue arises when we have a perfect fit for a sample, which performs poorly when we introduce new data points. The standard solution is to apply cross-validation (or use algorithms that avoid overfitting). In this method, we estimate model parameters on a part of the sample. The rest of the data is used to test and evaluate the model. This is actually a simplified explanation. There are more complex cross-validation schemes, a lot of which are supported by scikit-learn. To evaluate the model, we can compute appropriate evaluation metrics. As you can imagine, there are many metrics, and these metrics can have varying definitions due to constant tweaking by practitioners. We can look up these definitions in books or Wikipedia. The important thing to remember is that the evaluation of a forecast or fit is not an exact science. The fact that there are so many metrics only confirms that.

[ 176 ] Chapter 7

We will set up the model with the scipy.optimize.leastsq() function using the first two lagged components we found in the previous section. We could have chosen a linear algebra function instead. However, the leastsq() function is more flexible and lets us specify practically any type of model. Set up the model as follows:

def model(p, x1, x10):

p1, p10 = p return p1 * x1 + p10 * x10

def error(p, data, x1, x10):

return data - model(p, x1, x10)

To fit the model, initialize the parameter list and pass it to the leastsq() function as follows:

def fit(data):

p0 = [.5, 0.5]

params = leastsq(error, p0, args=(data[10:], data[9:-1], data[:10]))[0] return params

Train the model on a part of the data:

cutoff = .9 * len(sunspots) params = fit(sunspots[:cutoff]) print "Params", params

The following are the parameters we get:

Params [ 0.67172672

0.33626295]

With these parameters, we will plot predicted values and compute various metrics. The following are the values we obtain for the metrics:

Root mean square error 22.8148122613 Mean absolute error 17.6515446503 Mean absolute percentage error 60.7817800736 Symmetric Mean absolute percentage error 34.9843386176 Coefficient of determination 0.799940292779

[ 177 ] Signal Processing and Time Series

Refer to the following graph for the end result:

It seems that we have many predictions that are almost spot-on, but also a bunch of predictions that are pretty far off. Overall, we don't have a perfect fit; however, it's not a complete disaster. It's somewhere in the middle.

The following code is in the ar.py file in this book's code bundle:

from scipy.optimize import leastsq import statsmodels.api as sm import matplotlib.pyplot as plt import numpy as np

def model(p, x1, x10):

p1, p10 = p return p1 * x1 + p10 * x10

def error(p, data, x1, x10):

return data - model(p, x1, x10)

def fit(data):

p0 = [.5, 0.5]

[ 178 ] Chapter 7

params = leastsq(error, p0, args=(data[10:], data[9:-1], data[:-10]))[0] return params

data_loader = sm.datasets.sunspots.load_pandas() sunspots = data_loader.data["SUNACTIVITY"].values

cutoff = .9 * len(sunspots) params = fit(sunspots[:cutoff]) print "Params", params

pred = params[0] * sunspots[cutoff-1:-1] + params[1] *

sunspots[cutoff-10:-10] actual = sunspots[cutoff:] print "Root mean square error", np.sqrt(np.mean((actual - pred) **

2)) print "Mean absolute error", np.mean(np.abs(actual - pred)) print "Mean absolute percentage error", 100 * np.mean(np.abs(actual - pred)/actual) mid = (actual + pred)/2 print "Symmetric Mean absolute percentage error", 100 * np.mean(np.abs(actual - pred)/mid) print "Coefficient of determination", 1 - ((actual - pred) **

2).sum()/ ((actual - actual.mean()) ** 2).sum() year_range = data_loader.data["YEAR"].values[cutoff:] plt.plot(year_range, actual, 'o', label="Sunspots") plt.plot(year_range, pred, 'x', label="Prediction") plt.grid(True) plt.xlabel("YEAR") plt.ylabel("SUNACTIVITY") plt.legend() plt.show()

## 07. ARMA models

ARMA models are often used to forecast a time series. These models combine autoregressive and moving average models (see http://en.wikipedia.org/wiki/ Autoregressive%E2%80%93moving-average_model). In moving average models, we assume that a variable is the sum of the mean of the time series and a linear combination of noise components.

[ 179 ] Signal Processing and Time Series

The autoregressive and moving average models can have different orders. In general, we can define an ARMA model with p autoregressive terms and q moving average terms as follows:

x t = c + ∑ i = 1 p a i x t − i + ∑ i = 1 q bi ε t − i +∈t 

In the preceding formula, just like in the autoregressive model formula, we have a constant and a white noise component; however, we try to fit the lagged noise components as well.

Fortunately, it's possible to use the statsmodelssm.tsa.ARMA() routine for this analysis. Fit the data to an ARMA(10,1) model as follows:

model = sm.tsa.ARMA(df, (10,1)).fit()

Perform a forecast (statsmodels uses strings a lot):

prediction = model.predict('1975', str(years[-1]), dynamic=True)

Refer to the following plot for the end result:

[ 180 ] Chapter 7

The fit is poor because frankly, we overfit the data. The simpler model in the previous section worked much better. The example code can be found in the arma.py file in this book's code bundle:

import pandas as pd import matplotlib.pyplot as plt import statsmodels.api as sm import datetime

data_loader = sm.datasets.sunspots.load_pandas() df = data_loader.data years = df["YEAR"].values.astype(int) df.index = pd.Index(sm.tsa.datetools.dates_from_range(str(years[0]), str(years[-1]))) del df["YEAR"]

model = sm.tsa.ARMA(df, (10,1)).fit() prediction = model.predict('1975', str(years[-1]), dynamic=True)

df['1975':].plot() prediction.plot(style='--', label='Prediction') plt.legend() plt.show()

## 08. Generating periodic signals

Many natural phenomena are regular and trustworthy like an accurate clock.

Some phenomena exhibit patterns that seem regular. A group of scientists found three cycles in the sunspot activity with the Hilbert-Huang transform (see http:// en.wikipedia.org/wiki/Hilbert%E2%80%93Huang_transform). The cycles have a duration of 11, 22, and 100 years approximately. Normally, we would simulate a periodic signal using trigonometric functions such as a sine function. You probably remember a bit of trigonometry from high school. That's all we need for this example. Since we have three cycles, it seems reasonable to create a model, which is a linear combination of three sine functions. This just requires a tiny adjustment of the code for the autoregressive model. Refer to the periodic.py file in this book's code bundle for the following code:

from scipy.optimize import leastsq import statsmodels.api as sm import matplotlib.pyplot as plt import numpy as np

[ 181 ] Signal Processing and Time Series

def model(p, t):

C, p1, f1, phi1 , p2, f2, phi2, p3, f3, phi3 = p return C + p1 * np.sin(f1 * t + phi1) + p2 * np.sin(f2 * t + phi2) +p3 * np.sin(f3 * t + phi3)

def error(p, y, t):

return y - model(p, t)

def fit(y, t):

p0 = [y.mean(), 0, 2 * np.pi/11, 0, 0, 2 * np.pi/22, 0, 0, 2 *

np.pi/100, 0]

params = leastsq(error, p0, args=(y, t))[0] return params

data_loader = sm.datasets.sunspots.load_pandas() sunspots = data_loader.data["SUNACTIVITY"].values years = data_loader.data["YEAR"].values

cutoff = .9 * len(sunspots) params = fit(sunspots[:cutoff], years[:cutoff]) print "Params", params

pred = model(params, years[cutoff:]) actual = sunspots[cutoff:] print "Root mean square error", np.sqrt(np.mean((actual - pred) **

2)) print "Mean absolute error", np.mean(np.abs(actual - pred)) print "Mean absolute percentage error", 100 * np.mean(np.abs(actual - pred)/actual) mid = (actual + pred)/2 print "Symmetric Mean absolute percentage error", 100 * np.mean(np.abs(actual - pred)/mid) print "Coefficient of determination", 1 - ((actual - pred) **

2).sum()/ ((actual - actual.mean()) ** 2).sum() year_range = data_loader.data["YEAR"].values[cutoff:] plt.plot(year_range, actual, 'o', label="Sunspots") plt.plot(year_range, pred, 'x', label="Prediction") plt.grid(True) plt.xlabel("YEAR") plt.ylabel("SUNACTIVITY") plt.legend() plt.show()

[ 182 ] Chapter 7

We get the following output:

Params [ 47.18800285 28.89947419 0.56827284 6.51168446

4.55214999

0.29372077 -14.30926648 -18.16524041 0.06574835 -4.37789602] Root mean square error 59.5619175499 Mean absolute error 44.5814573306 Mean absolute percentage error 65.1639657495 Symmetric Mean absolute percentage error 78.4477263927 Coefficient of determination -0.363525210982

The first line displays the coefficients of the model we attempted. We have a mean absolute error of 44, which means that we are off by that amount in either direction on average. We also want the coefficient of determination to be as close to one as possible to have a good fit. Instead, we get a negative value, which is undesirable. Refer to the following graph for the end result:

[ 183 ] Signal Processing and Time Series

## 09. Fourier analysis

Fourier analysis is based on the Fourier series named after the mathematician Joseph Fourier. The Fourier series is a mathematical method used to represent functions as an infinite series of sine and cosine terms. The functions in question can be real or complex valued:

χ [ t ] e − i ωt ∑t =−∞ ∞ 

The most efficient algorithm for Fourier analysis is the Fast Fourier Transform (FFT). This algorithm is implemented in SciPy and NumPy. When applied to the time series data, the Fourier analysis transforms maps onto the frequency domain, producing a frequency spectrum. The frequency spectrum displays harmonics as distinct spikes at certain frequencies. Music, for example, is composed from different frequencies with the note A at 440 Hz. The note A can be produced by a pitch fork. We can produce this and other notes with musical instruments such as a piano. White noise is a signal consisting of many frequencies, which are represented equally. White light is a mix of all the visible frequencies of light, also represented equally.

In the following example, we will import two functions (refer to fourier.py):

from scipy.fftpack import rfft from scipy.fftpack import fftshift

The rfft() function performs FFT on real-valued data. We could also have used the fft() function, but it gives a warning on this particular dataset. The fftshift() function shifts the zero-frequency component (the mean of the data) to the middle of the spectrum, for better visualization. We will also have a look at a sine wave because that is easy to understand. Create a sine wave and apply the FFT to it:

t = np.linspace(-2 * np.pi, 2 * np.pi, len(sunspots)) mid = np.ptp(sunspots)/2 sine = mid + mid * np.sin(np.sin(t))

sine_fft = np.abs(fftshift(rfft(sine))) print "Index of max sine FFT", np.argsort(sine_fft)[-5:]

The following is the output that shows the indices corresponding to maximum amplitudes:

Index of max sine FFT [160 157 166 158 154]

[ 184 ] Chapter 7

Perform FFT on the sunspots data:

transformed = np.abs(fftshift(rfft(sunspots))) print "Indices of max sunspots FFT", np.argsort(transformed)[-5:]

The five largest peaks in the spectrum can be found at the following indices:

Indices of max sunspots FFT [205 212 215 209 154]

The largest peak is situated at 154 too. Refer to the following plot for the end result:

The complete code is located in the fourier.py file in this book's code bundle:

import numpy as np import statsmodels.api as sm import matplotlib.pyplot as plt from scipy.fftpack import rfft from scipy.fftpack import fftshift

data_loader = sm.datasets.sunspots.load_pandas() sunspots = data_loader.data["SUNACTIVITY"].values

t = np.linspace(-2 * np.pi, 2 * np.pi, len(sunspots)) mid = np.ptp(sunspots)/2

[ 185 ] Signal Processing and Time Series

sine = mid + mid * np.sin(np.sin(t))

sine_fft = np.abs(fftshift(rfft(sine))) print "Index of max sine FFT", np.argsort(sine_fft)[-5:]

transformed = np.abs(fftshift(rfft(sunspots))) print "Indices of max sunspots FFT", np.argsort(transformed)[-5:]

plt.subplot(311) plt.plot(sunspots, label="Sunspots") plt.plot(sine, lw=2, label="Sine") plt.grid(True) plt.legend() plt.subplot(312) plt.plot(transformed, label="Transformed Sunspots") plt.grid(True) plt.legend() plt.subplot(313) plt.plot(sine_fft, lw=2, label="Transformed Sine") plt.grid(True) plt.legend() plt.show()

## 10. Spectral analysis

In the previous section, we charted the amplitude spectrum of the dataset. The power spectrum of a physical signal visualizes the energy distribution of the signal. We can modify the code easily to plot the power spectrum, just by squaring the values as follows:

plt.plot(transformed ** 2, label="Power Spectrum")

The phase spectrum visualizes the phase (the initial angle of a sine function) and can be plotted as follows:

plt.plot(np.angle(transformed), label="Phase Spectrum")

[ 186 ] Chapter 7

Refer to the following graph for the end result:

Please refer to the spectrum.py file in this book's code bundle for the complete code.

## 11. Filtering

Filtering is a type of signal processing, which involves removing or suppressing a part of the signal. After applying FFT, we can filter high or low frequencies, or we can try to remove the white noise. White noise is a random signal with a constant power spectrum and as such doesn't contain any useful information. The scipy. signal package has a number of utilities for filtering. In this example, we will demonstrate a small sample of these routines:

• The median filter calculates the median in a rolling window (see http://en.wikipedia.org/wiki/Median_filter). It's implemented by the medfilt() function, which has an optional window size parameter.

• The Wiener filter removes noise using statistics (see http://en.wikipedia. org/wiki/Wiener_filter). For a filter g(t) and signal s(t), the output is calculated with the convolution (g * [s + n])(t). It's implemented by the wiener() function. This function also has an optional window size parameter.

[ 187 ] Signal Processing and Time Series

• The detrend filter removes a trend. This can be a linear or constant trend.

It's implemented by the detrend() function.

Please refer to the filtering.py file in this book's code bundle for the following code:

import statsmodels.api as sm import matplotlib.pyplot as plt from scipy.signal import medfilt from scipy.signal import wiener from scipy.signal import detrend

data_loader = sm.datasets.sunspots.load_pandas() sunspots = data_loader.data["SUNACTIVITY"].values years = data_loader.data["YEAR"].values

plt.plot(years, sunspots, label="SUNACTIVITY") plt.plot(years, medfilt(sunspots, 11), lw=2, label="Median") plt.plot(years, wiener(sunspots, 11), '--', lw=2, label="Wiener") plt.plot(years, detrend(sunspots), lw=3, label="Detrend") plt.xlabel("YEAR") plt.grid(True) plt.legend() plt.show()

Refer to the following graph for the end result:

## Summary

In this chapter, the time series examples used annual sunspot cycles data.

You learned that it's common to try to derive a relationship between a value and another data point or combination of data points a fixed number of periods in the past, in the same time series.

A moving average specifies a window of previously seen data, which is averaged each time the window slides forward by one period. In the pandas API, the rolling_ window() function provides the window functions functionality with different values of the win_type string parameter corresponding to different window functions.

Cointegration is similar to correlation and is a metric to define the relatedness of two time series. In regression setups, we frequently encounter the problem of overfitting. This issue arises when we have a perfect fit for a sample, which performs poorly when we introduce new data points. To evaluate a model, we can compute appropriate evaluation metrics.

Databases are an important tool for data analysis. Relational databases have been around since the 1970s. Recently, NoSQL databases have become a viable alternative. The next chapter, Chapter 8, Working with Databases, contains information about the various databases (relational and NoSQL) and related APIs.
