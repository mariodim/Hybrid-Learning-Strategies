### Getting Started

## Hybrid Learning Strategies for Multivariate Time Series Forecasting of Network Quality Metrics
We release an original real-world dataset used to perform the so-called "Multivariate time series prediction" by combining statistical techniques (e.g. VAR) with Deep Learning techniques. The dataset contains several features of cellular traffic organized into time series. The goal is to exploit statistical and learning-based techniques to predict the future behavior of a given feature. If you dataset, code, or part of them, please cite the following work: https://www.sciencedirect.com/science/article/pii/S138912862400118X

## Cellular Traffic collection in a real environment

The equipment we used to build the real-world dataset includes:
- 1 mobile device equipped with Linphone (open-source softphone suppoorting RTCP-XR protocol) and a LTE-Advanced mobile SIM;
- 1 standard PC equipped with: i) Linphone softphone, ii) Wireshark to capture the network traffic in .pcap format.

The area where we performed experiments is near Salerno city (Italy), with a density of about 2000 people/sqKM.
The mobile operator is Vodafone. Currently (Sept. 2023), the radio coverage is almost entirely in LTE-Advanced (also marketed as 4G+).

## Dataset Construction

The Dataset contains network traffic gathered in a real cellular environment.  
The whole dataset includes 8 VoIP conversation grouped per codec: G.722, G.729, GSM, G.711, Mpeg4-16, OPUS, Speex-8, Speex-16.

The processed data files are available at: https://github.com/mariodim/ml_mobile_dataset/blob/main/ML_TimeSeries_DATASETS.zip
under the subfolder named "mobile".

Each conversation contains 6 temporal features:
- MOS (Mean Opinion Score) --> measures the call quality (expressed in a pure value between 1 and 5)
- BW (Bandwidth) --> measures the bandwidth consumed by a voice call ( expressed in kb/s)
- RTT (Round Trip Time) --> measures the interval beetwen a sent and a received packet (expressed in ms)
- JTR (Jitter) --> measures the inter-packet jitter (expressed in ms)
- DJB (De-jittering Buffer) --> measures the buffer lenght used to reduce jitter (expressed in ms)
- SNR (Signal-to-Noise ratio) --> measures the objective quality of the communication channel (expressed in dB)


## Usage

Each sub-dataset must be uploaded into our Python routine available at: https://colab.research.google.com/drive/1MgiA5uNF4lF5kEsIgAo4W8Jbm1BqlQYL?usp=sharing 

After uploaded a sub-dataset (e.g. mob_g722.txt, meaning that the traffic is collected within the mobile scenario and the codec used is G.722), set the parameters in the first "cell" of the Python code:  

- filename --> insert the name of the uploaded file (e.g. "mob_g722.txt");
- train_size --> you can choose the percentage of training size (the test size is set accordingly);
- param --> you can define the size of your DL network (number of dense neurons, number units);
- models --> you can choose which model you want to use: 0 = LSTM ; 1 = VAR+LSTM ; 2 = CNN ; 3 = VAR+CNN ; 4 = GRU ; 5 = VAR+GRU
- n_past (in the run definition) --> the lag "p" obtained by applying Akaike Criterion. For codec G.722, p=12.

With the default values set, you have just to upload the file, set its name and run.

## Output

Output files include:  

- TXT files containing time series predictions per technique --> e.g. the output file mob_g722_cnn.txt is a 12-column file in this format: column #1 contains original values of MOS, column #2 contains predicted values of MOS, column 2 contains original values of BW, column #2 contains predicted values of BW, and so forth. Once exported, such files can be obviously used to reproduce the plots through different plot tools;
 
- Information about MSE and MAE per each technique

- Information about training time per each technique (directly shown in the output code).
