\documentclass[conference]{IEEEtran}
\IEEEoverridecommandlockouts
\DeclareUnicodeCharacter{2212}{\textminus}
\usepackage{placeins}
\usepackage{tabularx}
\usepackage{booktabs}
\usepackage{multirow}
\usepackage[utf8]{inputenc}
\usepackage{amsmath,amssymb,amsfonts}
\usepackage{algorithmic}
\usepackage{algorithm}
\usepackage{graphicx}
% \usepackage{cite} % REMOVE or KEEP COMMENTED - conflicts with natbib
\usepackage{subcaption}
\usepackage{textcomp}
\usepackage{xcolor}
\usepackage[numbers]{natbib}

\usepackage{hyperref}
\usepackage{url}
\usepackage{fancyhdr}
\usepackage{float}
\usepackage{flushend}
\usepackage[bordercolor=gray!5,textcolor=red!100, backgroundcolor=yellow!20,textsize=scriptsize, textwidth=.65in]{todonotes}
% Define \todoi command for italic todo notes
\newcommand{\todoi}[2][]{\todo[#1]{\textit{#2}}}
\usepackage{comment}
\usepackage{multirow}
\usepackage{tabularx}
\usepackage{array}
\usepackage{longtable}
\usepackage{afterpage}
\usepackage{stfloats}
\usepackage{booktabs}
\usepackage{balance}

\usepackage[bordercolor=gray!5,textcolor=red!100, backgroundcolor=yellow!20,textsize=scriptsize, textwidth=.65in]{todonotes}


\usepackage{soul}
\newcommand{\cmnt}[1]{{\sethlcolor{cyan}\hl{\textit{(#1)}}}}
\usepackage{gensymb}
\usepackage{makecell}
\usepackage{siunitx}
\newcolumntype{R}[1]{S[table-format=#1]}

\def\BibTeX{{\rm B\kern-.05em{\sc i\kern-.025em b}\kern-.08em
    T\kern-.1667em\lower.7ex\hbox{E}\kern-.125emX}}

\begin{document}
\title {Comparative Analysis of Large Language Models for Sentiment and Emotion Modeling in Text-based Conversations}


\makeatletter
\newcommand{\linebreakand}{%
  \end{@IEEEauthorhalign}
  \hfill\mbox{}\par
  \mbox{}\hfill\begin{@IEEEauthorhalign}
}
\makeatother

%Samia Sharmin Lima -23-50408-1@student.aiub.edu
%Ismail Hossain fahim -
%MD Ali Haider

\author{\IEEEauthorblockN{MD Ali Haider}%1\textsuperscript{st} 
\IEEEauthorblockA{\textit{Department of Computer Science} \\
\textit{American International University-Bangladesh}\\
Dhaka, Bangladesh \\
23-50011-1@student.aiub.edu}
\and
\IEEEauthorblockN{Samia Sharmin Lima}
\IEEEauthorblockA{\textit{Department of Computer Science} \\
\textit{American International University-Bangladesh}\\
Dhaka, Bangladesh \\
23-50408-1@student.aiub.edu} 
\linebreakand
\IEEEauthorblockN{ Ismail Hossain Fahim}
\IEEEauthorblockA{\textit{Department of Computer Science} \\
\textit{American International University-Bangladesh}\\
Dhaka, Bangladesh \\
23-50009-1@student.aiub.edu}
\and
\IEEEauthorblockN{4\textsuperscript{th} Fname Lname}
\IEEEauthorblockA{\textit{Department of Computer Science} \\
\textit{American International University-Bangladesh}\\
Dhaka, Bangladesh \\
24-93526-3@student.aiub.edu}
\linebreakand
\IEEEauthorblockN{5\textsuperscript{th} Fname Lname}
\IEEEauthorblockA{\textit{Department of Computer Science} \\
\textit{American International University-Bangladesh}\\
Dhaka, Bangladesh \\
24-12345-3@student.aiub.edu}
\and
\IEEEauthorblockN{ Kamruddin Nur}
\IEEEauthorblockA{\textit{Department of Computer Science} \\
\textit{American International University-Bangladesh}\\
Dhaka, Bangladesh \\
kamruddin@aiub.edu}

}

% % Configure header and footer
% \fancypagestyle{firstpage}{
%     \fancyhf{} % Clear all header and footer fields
%     % Header
%     \fancyhead[L]{2025 International Conference on \ldots , date of conference, place of conference, city, country}
%     % Footer
%     \fancyfoot[L]{979-8-3503-5750-9/25/\$31.00 ©2025 IEEE}
%     \renewcommand{\headrulewidth}{0pt} % Remove header line
%     \renewcommand{\footrulewidth}{0pt} % Remove footer line
% }

\maketitle 
%\thispagestyle{firstpage}

\begin{abstract}

%New abstract %
The significance of emotions in text-based communication has become increasingly prominent in recent years, attributed to the rise of conversational AI in applications such as chatbots and virtual assistants. Most sentiment analysis methods are centred on finding either a positive or negative feeling. However, emotions cannot be analyzed using the
traditional techniques. Moreover, the majority of the investigations have concentrated solely on the assessment of emotion recognition utilising a singular language model. This has made it harder to understand how well different Large Language Models (LLMs) do at finding emotions in text-based communication. This research has concentrated on addressing this deficiency by performing a comparative analysis of LLMs for sentiment and emotion modelling in text-based communication. The researchers utilised many well-known conversational datasets, including DailyDialog, MELD, IEMOCAP, and EmoryNLP, in this study. We used precision, recall, and F1-score to see how well the LLMs worked. The results
of the study have shown that LLMs have different capabilities
in emotion detection in text-based communication.
IndexTerms: Large Language Models (LLMs), Sentiment Analysis, Emotion Detection, Emotion Modelling, Text-based Communication, Conversational AI



%\textbf{\textit{IndexTerms} :} 




\end{abstract}

\begin{IEEEkeywords}
large language models (LLMs), sentiment analysis, emotion detection, emotion modeling, text-based communication , conversational AI
\end{IEEEkeywords}

\section{Introduction}
Large Language Models (LLMs) have entirely transformed the way natural language processing functions, particularly concerning how people feel and what they intend in written dialogues. Sentiment analysis used to be mostly concerned with putting some text into large categories, such as positive, negative, or neutral. However, since human emotions are so complex, we must be in a position to recognize them in a finer detail, such as the various emotional conditions such as joy, anger, sadness, and fear. It is extremely essential in most areas such as in healthcare, finance, education, and customer services to learn how people feel, what they do and how they relate with other people.\cite{kastrati-2025,lecourt-2025}

New models in transformer architecture, particularly LLMs like GPT-4, MobileBERT, and Gemini Pro, have boosted the advances in sentiment and emotion. modeling. These models are superior in capturing contextual and linguistic nuances, frequently. applying zero-shot and few-shot learning to do well even in low-resource scenarios or less commonly studied languages\cite{kastrati-2025,nasution-2025}. We can take studies benchmarking open as an example. compared to proprietary systems reveal that some mid-sized LLMs can be effectively trained on source large datasets. can be a close approximation of ChatGPT-4 in sentiment of Indonesian tweets and classification of emotions, emphasizing the availability of high-performing models outside. commercial products which are well known.[*3]

In tandem with these performance boosts, implementing emotion and sentiment analysis on. 
resource constrained environments like edge devices has become a hotbed of concern. 
New multitask learning models combining smaller model such as MobileBERT. 
and DistilBERT take advantage of adaptive learning strategies and prototypical networks to preserve. 
competitive accuracy and subject to computational constraints. Such efficient designs 
enable emotion and sentiment recognition in real time in applications as far along the spectrum as affective. 
healthcare monitoring to computing\cite{hussain-2025}.



Moreover, stability and robustness of LLM-based systems of sentiment analysis is still. 
topics of current research. As an example, ChatGPT-based sentiment models show. 
a high degree of variance, and sensitivity to small adversarial examples, which is problematic in quality. 
durability and dependability of sensitive applications. These findings highlight the need for 
strong operational procedures and further testing on hostile terms\cite{ouyang-2024}.

Another frontier is the intersection of explainability and LLMs, as the nature of the opaque nature of. 
these complicated frameworks tend to constrain trust and interpretability. Research applying Explainable 
Pre-trained LLMs are evaluated using artificial intelligence (XAI) techniques, which will provide information about underlying. A task in multilingual sentiment and emotion recognition, which offers decision mechanisms. 
transparency and possible model debugging and refinement possibilities [*2]. Moreover, integrating personalized and contextual information via multi-source fusion approaches additionally develops emotion recognition that is smooth, taking into account the user-specific behavior. and context of conversation, beyond the models of analysis at isolated sentences\cite{ngo-2025}.

LLMs have transformed sentiment analysis to gain insight into customers in applied fields. 
analysis of financial markets, and education. Aspect-Based Sentiment Analysis (ABSA) 
GPT-4 leverage proves to be able to read nudge sentiments in. 
hospitality is more efficient in reviews than traditional fuzzy logic or manual approaches, therefore. 
enhancing organizational responsiveness \cite{agua-2025}. Financial sentiment analysis, likewise, is the study of the emotional aspects of the financial market. 
It is possible to utilize more accurate models based on LLMs like FinBERT, LLaMA, and GPT-3 to achieve this. 
predicting the stock and cryptocurrency market, optimizing investment strategies with 
better awareness of market sentiments in news articles [*8], [*9]. In educational 
contexts, transformer models such as IndoBERT demonstrate a better reflexion of student. 
feedback of evaluation, which provides feedback that can lead to a change in teaching and improvement. 
Curriculum development is a complex process [*10].

Nevertheless, in spite of these advancements, there is a variety of model architectures and training approaches. 
has different merits and demerits. Comparative analyses indicate that whereas certain ones have excelled. 
At times, traditional methods (e.g., TextBlob) do well on some metrics compared to LLMs, such as. 
accuracy, transformer-based models have more balance in terms of precision and recall. 
These lessons highlight the need to use models that are in line with particular task. 
requirements and contexts of operations [*11].
%break-time ~ismail


The key contributions of this study are as follows:
\begin{enumerate}
    \item Proposed a deep learning based application for detecting anemia signs from eye conjunctiva images using improved YOLOv9.
    \item Replaced AConv with standard Conv in layers 3, 5, and 9 of the backbone and layer 19 of the neck, reducing layers and parameters. This led to improved inference speed compared to the default YOLOv9s. 
    \item Compared the proposed YOLOv9 model performance with YOLOv8 through YOLOv12 and achieved the highest F1-score of 1.00 and mAP@50 of 0.995, supporting real-time anemia detection. 
\end{enumerate}

The remainder of this paper is organized as follows. Section \ref{sec:RW} reviews prior work on non-invasive anemia detection. Section \ref{sec:PS} details the proposed method, including data collection, preprocessing, and augmentation. Section \ref{sec:ERD} analyzes model performance. Section \ref{SEC: limF} discusses limitations and future work.
Finally, Section \ref{sec:con} concludes the study. 

\section{Related Works} \label{sec:RW}

Deep learning, particularly CNNs and advanced models like ResNet and VGG, has proven effective in non-invasive anemia detection using conjunctival images. Recently, real-time object detection models like YOLO have gained attention for their suitability in mobile and low-resource healthcare settings \cite{Bijit}.

\begin{figure*} [ht]
	\centering
	\includegraphics[width=0.8\linewidth]{Model.png}
	\caption{Workflow of the proposed model training, validation, and testing on the dataset.}
	\label{ProposedModel}
\end{figure*}

%\citeauthor{bib5} \cite{bib5} 
\citet{bib5}  proposed an automated method for anemia detection using non-invasive images of the palpebral conjunctiva. They evaluated the approach using three CNN architectures: AlexNet, ResNet-50, and MobileNetV2. Among them, ResNet-50 achieved the highest accuracy of 97.94\%, followed by MobileNetV2 with 97.19\%, and AlexNet with 89.93\%. \citet{bib6} proposed a smartphone-based anemia detection model using palpebral conjunctiva images. They expanded a dataset of 764 images to 4,315 using DCGAN for augmentation. Multiple machine learning (SVM, KNN, Naïve Bayes, Decision Tree) and deep learning models (GoogLeNet, VGG16, ResNet-50) were tested, along with ensemble techniques. The stacking ensemble model achieved the best results, with 89.48\% accuracy, 88\% precision, and 0.97 AUC. \citet{bib8} proposed a non-invasive method for anemia detection using smartphone images analyzed through MATLAB. Tested on 19 patients, it achieved 78.9\% accuracy, offering a low-cost solution. \citet{10534530} introduced UNBCSM, a U-Net-based model with a ResNet-34 backbone for offline anemia screening using smartphone eye images. Trained on 135 manually annotated samples, the model was optimized with fewer max-pooling layers, achieving a mean IoU of 96\% (training) and 85.7\% (validation). \citet{Khan2024} proposed a deep learning approach for anemia detection using retinal fundus images from 2,265 participants. InceptionV3 achieved 98.6\% accuracy and an AUC of 0.98, while VGG16 and ResNet50 showed comparable performance. Combining clinical metadata further improved hemoglobin prediction. \citet{Ramzan2024} investigated machine learning approaches for noninvasive anemia detection using multi-modal data (textual and image). Traditional models like logistic regression, decision trees, and SVMs were compared with advanced models incorporating spatial attention mechanisms. Their proposed AlexNet with Multiple Spatial Attention achieved a remarkable 99.58\% accuracy.

The summary of the related works is presented in Table~\ref{tab:related_work}. 

\begin{table*}[!b]
\centering
\caption{Summary of related studies on software defect prediction}
\label{tab:related_work}
\resizebox{\textwidth}{!}{%
\begin{tabular}{c c p{3.6cm} p{4.2cm} p{3.2cm} p{4.6cm}}
\toprule
\textbf{Ref.} & \textbf{Year} & \textbf{Dataset} & \textbf{Method / Algorithm} & \textbf{Accuracy} & \textbf{Limitations} \\
\midrule

{\cite{bib1}} &
2025 &
Synthetic dataset (5,000 samples) &
RF, SVM, Gradient Boosting with Deep Learning; SMOTE &
Accuracy: 94.7\%; Precision: 93.2\%; Recall: 96.1\%; AUC: 0.978 &
Synthetic dataset; limited real-world validation \\

{\cite{bib2}} &
2024 &
ApacheJIT (106,674 commits) &
MLP with SMOTE; SHAP-based interpretation &
82.08\% &
High computational cost; single dataset \\

{\cite{bib3}} &
2024 &
LSTM outperforms ML and DL baselines on unified defect data. &
ML, DL, and LSTM comparison. &
LSTM: 87\%. &
No feature selection; limited tuning; single dataset. \\

{\cite{bib4}} &
2023 &
NASA CM1 &
Feature selection, K-means, SVM, RF, NB, PSO-based ensembles &
SVM: 99\%; SVM-PSO: 99.80\% &
Small dataset; limited generalization \\

{\cite{bib5}} &
2023 &
Multiple NASA datasets (JM1, PC2, etc.) &
Random Forest, AdaBoost, Bagging, SVM & JM1: 89.80\%;
PC2: 99.64\% &
Computational complexity; scalability concerns \\

{\cite{bib6}} &
2023 &
NASA JM1 &
SVM, Logistic Regression, MLP, 1D CNN &
CNN: 97.38\%; MLP: 93.47\% &
Single dataset; no cross-project validation \\

\bottomrule
\end{tabular}}
\end{table*}


\section{Proposed System}\label{sec:PS}
The proposed system is presented in Figure \ref{ProposedModel}, 
which consists of six parts: i) image acquisition, ii) dataset preparation and annotation, iii) dataset splitting and preprocessing, iv) data augmentation, v) deep learning model construction, and vi) performance analysis.

\subsection{Image Acquisition}
The image acquisition is the first foundational step in building an effective anemia detection model. For this study, we utilized open-source datasets available on Roboflow to construct a comprehensive dataset focused on the conjunctiva region of the eye \cite{pallor-detection_dataset} \footnote{https://universe.roboflow.com/md-nawshin-navin/pallor-detection}. The initial dataset labeled under a single class, ``Conjunctiva\_Pallor'', which visually represents signs of anemia. To balance the dataset and ensure reliable classification, we integrated an additional dataset under the class ``Normal\_Conjunctiva''. Both datasets were forked and combined to form a custom binary-class dataset for this study.

\subsection{Dataset Preparation and Annotation}
This subsection outlines the essential steps involved in preparing the dataset, including data annotation, preprocessing, and augmentation. We used the Roboflow platform, which offers a variety of functions, such as data annotation, data preprocessing, model training, as well as deployment. Each image was manually annotated to define the region of interest (ROI)—specifically the palpebral conjunctiva—to ensure consistent labeling across the dataset. Accurate ROI selection is critical for improving the model's ability to focus on clinically relevant features. Data preprocessing is a crucial step to enhance image quality and standardize the input for deep learning analysis, and it requires large volumes of data to learn complex patterns effectively. 

\subsection{Dataset Splitting and Preprocessing}

In this phase, we initially split the annotated dataset into 87\% for training (777 images), 6\% for validation (168 images), and 6\% for testing (166 images). This distribution was chosen to maximize the model’s learning efficiency while ensuring a fair and reliable evaluation of its performance. Data preprocessing, a crucial step in deep learning workflows, involved standard techniques such as noise reduction, contrast enhancement, and image resizing. Specifically, we applied auto-orientation, resized all images to 640 × 640 pixels, and adjusted image contrast to enhance visual quality and consistency across the dataset.

\subsection{Data Augmentation}
The augmentation phase is essential for expanding the dataset and mitigating overfitting, particularly due to the limited number of original images. To enhance the robustness and generalization capability of the detection model, we applied a variety of data augmentation techniques to the training set. These included rotation, horizontal and vertical flipping, brightness and contrast adjustments, zooming, and scaling—each simulating diverse real-world imaging conditions. Labeling eye conjunctiva images presents significant challenges due to variations in lighting, age, gender, and viewing angles, all of which can impact model accuracy. To address these issues, data augmentation was employed to increase dataset diversity and improve the model's ability to generalize across different conditions. Following augmentation, the training dataset was expanded to 2,272 images, ensuring a more comprehensive and representative sample for model training. Table \ref{tab1} presents the summary statistics of the anemia disease detection dataset, which consists of two binary classes: ``Conjunctiva\_Pallor'' (indicating potential anemia) and ``Normal\_Conjunctiva'' (healthy cases).

\begin{table}[ht]
\caption{Anemia disease detection dataset statistics}
\label{tab1}
\centering
\begin{tabular*}{\textwidth}{
p{3.6cm}
>{\centering\arraybackslash}p{0.8cm}
>{\centering\arraybackslash}p{1cm}
>{\centering\arraybackslash}p{0.6cm}
>{\centering\arraybackslash}p{0.5cm}
} 
\cline{1-5}
Image Categories& Training Count  & Validation Count & Test Count & Total \\
\cline{1-5}
Conjunctiva\_Pallor (Original) & 395  & 59& 110 & \multirow{2}{*}{1111} \\
\cline{1-4}
Normal\_Conjunctiva (Original)& 382  &  109 & 56 & \\
\cline{1-5}
Augmented 3x (Training) & 2272  & 168 & 166 &  2606\\
\cline{1-5}
\end{tabular*}
\end{table}
\vspace{-8.5pt}
\subsection{Deep Learning Model YOLOv9}
This paper presents an improved YOLOv9 deep learning model for anemia detection and classification, featuring a novel architecture with fewer parameters (Param), reduced calculations (FLOPs), and improved performance. The model consists of four key components: the information bottleneck concept, reversible functions, programmable gradient information (PGI), and the generalized efficient layer aggregate network (GELAN) \cite{bib22}. We selected YOLOv9 rather than later YOLO versions for its efficient PGI and lightweight design, making it ideal for edge devices. In addition, YOLOv10, v11 and v12 deos not produce better results for our purpose.  

The proposed improved YOLOv9 model is designed to address the key challenges in object identification, particularly network architecture efficiency and information loss. We modified the default YOLOv9s architecture by replacing all AConv (Adaptive Convolution) layers in the backbone (specifically at layers 3, 5, and 7) and the neck (layer 19) with standard Conv layers. While AConv is designed to adaptively model complex spatial relationships, it often introduces computational overhead. In contrast, standard Conv layers are not only faster but also highly effective at extracting foundational features such as edges, textures, and fine-grained patterns, making them better suited for real-time applications. Table \ref{comparison} summarizes a comparative analysis between the default and proposed YOLOv9s models, detailing changes in model architecture, GFLOPs, number of parameters, and inference time. %This comparison highlights the effectiveness of the proposed changes in making the model more suitable for real-time Anemia detection and classification using eye conjunctiva images.
\begin{table}[ht]
\begin{center}
\caption{Comparison of default and modified YOLOv9s Model's architecture.}
\label{comparison}
\setlength{\tabcolsep}{3pt}
\begin{tabular}{p{65pt} 
>{\centering\arraybackslash}p{43pt} 
>{\centering\arraybackslash}p{34pt} 
>{\centering\arraybackslash}p{26pt} 
>{\centering\arraybackslash}p{49pt}}
\cline{1-5}
Model & No. of layers & Parameters & GFLOps & Inference (ms)\\
\cline{1-5}
Default YOLOv9 & 544 & 7,288,182 & 27.4 & 6.1  \\ \cline{1-5}
\textbf{Proposed YOLOv9} & \textbf{320} & \textbf{5,976,566} & \textbf{23.1} & \textbf{5.3} \\
\cline{1-5}
\end{tabular}
\end{center}
\end{table}
\vspace{-8.5pt}
\subsection{Performance Evaluation} 
The model's performance was evaluated using precision (P), recall (R), mean average precision (mAP), and F1-score. Precision measures the accuracy of predicted classes, which is denoted by Eq. \eqref{eq4}, while recall assesses how well true classes are identified by Eq. \eqref{eq5}. The mAP evaluates overall prediction accuracy by Eq. \eqref{eq6}, and the F1-score represents the harmonic mean of precision and recall denoted by Eq. \eqref{eq7}.

\begin{equation}
    P = \left(\frac{T_{P}}{T_{P}+F_{P}}  \right)\times 100
    \label{eq4}
\end{equation}
\begin{equation}
    R = \left(\frac{T_P}{T_P+F_N} \right) \times 100
    \label{eq5}
\end{equation}
\begin{equation}
    mAP=\frac{ \sum_{i=1}^{Q}\left(AP_i \right)}{Q}
    \label{eq6}
\end{equation}

\begin{equation}
    F1-score =2\times \frac{\left(P \times R\right)}{\left(P+R\right)}
    \label{eq7}
\end{equation}
\begin{comment}
\begin{equation}
    AP_i = \left(\frac{\frac{T_P}{T_P+F_P}}{N} \right)*100
    \label{eq8}
\end{equation}
\end{comment}

\section{Results and Discussions } \label{sec:ERD}
This section presents the scientific findings of the proposed system with clear interpretations. It begins with a description of the system configurations, followed by an analysis of the simulation results. %The proposed model compares with other YOLO series.
\begin{figure*}[htp]
	\centering
	\includegraphics[width=0.85\linewidth]{results.png}
	\caption{Training graphs of the proposed model of anemia disease identification.}
	\label{traininggraph}
\end{figure*}

\begin{figure*}[htp]
\centering
       \begin{subfigure} [t]{0.45\textwidth}
            \centering
            \includegraphics[width=3.3in]{F1_curve.png} 
            \caption{}
            \label{subfig: 6A}      
       \end{subfigure}
       %\hspace{2cm}
       \hspace{1em}%
      % \hfill
       \begin{subfigure} [t]{0.45\textwidth}
            \centering
            \includegraphics[width=3.3in]{PR_curve.png}
            \caption{}
            \label{subfig: 6B}      
       \end{subfigure}
       \hfill
       \begin{subfigure} [t]{0.45\textwidth}
            \centering
            \includegraphics[width=3.3in]{confusion_matrix.png}
            \caption{}
            \label{subfig: 6C}      
       \end{subfigure}
       %\hspace{2cm}
       \hspace{1em}%
      % \hfill
       \begin{subfigure} [t]{0.45\textwidth}
            \centering            
            \includegraphics[width=3.3in]{confusion_matrix_normalized.png}
            \caption{}
            \label{subfig: 6D}      
       \end{subfigure}
    \caption{Proposed model performance metrics curves: (a) F1-score, (b) mAP@50, (c) Confusion matrix with instances, and (d) Normalized Confusion Matrix.}
    \label{fig:fig6}
\end{figure*}

\subsection{System Configuration} 
The proposed YOLOv9 model was utilized to detect anemia disease. To optimize and accelerate the training process, we leveraged a powerful NVIDIA L4 GPU with 12.75GB of RAM and 22700MiB capacity. The setup employed Python 3.10.12 runtime and CUDA 12.2.

\subsection{Hyperparameters}
The real-time detection of anemia using the proposed YOLOv9 model involves a set of training configurations and hyperparameters to ensure optimal performance. Table \ref{hyparam} summarizes the key training settings. Training was performed over 100 epochs using the Stochastic Gradient Descent (SGD) optimizer, chosen for its efficiency and stability when working with large-scale image datasets. A batch size of 32 was selected which provided a balance between memory efficiency. To reduce overfitting, a weight decay of 0.0005 was applied to prevent the model from relying on large parameter values.

\begin{table}[ht]
\begin{center}
\caption{Key training hyperparameters of the proposed model}
\label{hyparam}
\setlength{\tabcolsep}{3pt}
\begin{tabular}{p{75pt} 
>{\centering\arraybackslash}p{40pt} p{65pt} >{\centering\arraybackslash}p{40pt}}
\hline
Hyperparameters & Values & Hyperparameters & Values\\
\cline{1-4}
Initial Learning Rate & 0.01  &Optimizer & SGD                     \\ \cline{1-4}
Momentum& 0.937     & Batch size& 32                   \\ \cline{1-4}
Weight Decay & 0.0005   & Image Size & 640          \\  \cline{1-4}
%Epochs & 100           \\
\hline
\end{tabular}
\end{center}
\end{table}
\vspace{-9.5pt}


\subsection{Simulation Results} 
%We trained the dataset using the proposed model.  
The proposed model is the finest for real-time object detection in a variety of activities due to its speed, accuracy, and versatility. During the training period, we obtained the best result after 100 epochs. Figure \ref{traininggraph} shows the model training performance—followings were analyzed: mAP@50, mAP@50-95 (for the IoU and the thresholds of 50\%, 55\%,..., 95\%), Speed, and computations (GFLOPS). Table \ref{albumentation} displays the metrices, precision, recall, mAP@50, and mAP[50-95] after 100 epochs of training execution.

\begin{table}[ht]
\caption{Albumentations training results of the proposed model after executing 100 epochs}
\label{albumentation}
\begin{tabular*}{\textwidth}{
p{2.2cm}
>{\centering\arraybackslash}p{0.8cm}
>{\centering\arraybackslash}p{0.5cm}
>{\centering\arraybackslash}p{0.5cm}
>{\centering\arraybackslash}p{0.7cm}
>{\centering\arraybackslash}p{1.5cm}
} 
\cline{1-6}
Class & Instances  & P & R & mAP50 & mAP[50-95]\\
\cline{1-6}
Normal\_Conjunctiva & 110 & 0.999 & 0.995    &  0.995     & 0.865 \\ \cline{1-6}
Conjunctiva\_Pallor & 59    &  0.999     &     1   &   0.995  &    0.867 \\
\cline{1-6}
\end{tabular*}
\end{table}


The relationship between the accuracy of the model and the confidence level for each prediction is illustrated in Figure \ref{fig:fig6}, offering a complete evaluation of the reliability of the model. Figure \ref{subfig: 6A} presents the F1-score, which identifies the optimal confidence threshold that balances precision and recall. A maximum F1-score of 1.00 was achieved at a confidence level of 0.713, indicating perfect harmonic mean performance at this threshold. Figure \ref{subfig: 6B} displays the mAP at an IoU threshold of 0.50 (mAP@50), where the model achieved a high value of 0.995, confirming its precise localization and classification capabilities. Figures \ref{subfig: 6C} and \ref{subfig: 6D} provide confusion matrices that detail classification accuracy across the two classes: Normal\_Conjunctiva and Conjunctiva\_Pallor. Diagonal entries indicate correct classifications, demonstrating the model's robust prediction performance. Notably, the model achieved flawless detection for the Conjunctiva\_Pallor class, while only a single instance from the Normal\_Conjunctiva class was misclassified. %This suggests a slight bias toward detecting pathological cases more confidently—an advantageous trait in medical diagnostics, where false negatives could have serious implications. 
These visualizations collectively affirm the YOLOv9 model’s reliability, precision, and clinical applicability in anemia detection using conjunctival images.

To demonstrate the effectiveness of the trained model, the study projected anemia diseases from the test dataset. All tests were performed using the same environments and parameters. Figure \ref{fig:fig8} shows the observable outcomes of these assessments using the proposed model, displaying accurate detections. Figure \ref{subfig: 10A}–\ref{subfig: 10D} illustrates how well the suggested method identifies and classifies normal and conjunctival classes, however, the maximum detection confidence is approximately close to 0.98. The proposed model also demonstrates high efficiency, with an average preprocessing time of 0.3 ms and an inference time of 5.3 ms per image.

\begin{figure} [ht]
   \centering    
       \begin{subfigure}[t]{0.22\textwidth}
            \centering
            \includegraphics[height=2.5cm, width=0.9\textwidth]{r1.jpg}
            \caption{}
            \label{subfig: 10A}      
       \end{subfigure}
       \hfill
       \begin{subfigure}[t]{0.22\textwidth}
            \centering
            \includegraphics[height=2.5cm, width=0.9\textwidth]{r5.jpg}
            \caption{}
            \label{subfig: 10B}      
       \end{subfigure}
      \hfill
       \begin{subfigure}[t]{0.22\textwidth}
            \centering
            \includegraphics[height=2.5cm, width=0.9\textwidth]{r2.jpg}
            \caption{}
            \label{subfig: 10C}      
       \end{subfigure}
       \hfill
       \begin{subfigure}[t]{0.22\textwidth}
            \centering
            \includegraphics[height=2.5cm, width=0.9\textwidth]{r3.jpg}
            \caption{}
            \label{subfig: 10D}      
       \end{subfigure}
       \centering
       \caption{The proposed model's predicted results for normal and anemia disease from conjunctival images.}
       \label{fig:fig8}  %\label{fig:fig10} 
\end{figure}
To validate the effectiveness of the proposed YOLOv9 model, we conducted a performance comparison with other YOLO versions, including YOLOv8 through YOLOv12, based on the benchmark metrics mAP@50 and F1-score. As shown in Table \ref{modelCompare}, the proposed model, trained with the SGD optimizer, achieved superior results, attaining the highest mAP@50 and F1-score and Table \ref{existstudies} compares our model with existing methods, acheived 98.2\% enhanced accuracy, confirming the robustness in anemia detection.

\begin{table}[ht]
\caption{Comparing the proposed YOLOv9 performance with other YOLO models}
\label{modelCompare}
\begin{tabular*}{\textwidth}{
p{3cm}
>{\centering\arraybackslash}p{1.2cm}
>{\centering\arraybackslash}p{1.2cm}
>{\centering\arraybackslash}p{1.5cm}
}
\cline{1-4}
Model    & Optimizer & mAP@50 & F1-score\\
\cline{1-4}
YOLOv8s &  SGD  &  0.994 &  0.995 \\ \cline{1-4}
YOLOv9s (Default) &  SGD  &  0.993 &  0.996 \\ \cline{1-4}
YOLOv10s &  SGD  &  0.985 & 0.993 \\ \cline{1-4}
YOLOv11s &  SGD  &  0.994 & 0.993 \\ \cline{1-4}
YOLOv12s &  SGD  &  0.992 & 0.991 \\ \cline{1-4}
\textbf{Proposed YOLOv9s}
& \textbf{SGD}   & \textbf{0.995}   & \textbf{1.00}   \\ \cline{1-4}

\end{tabular*}
\end{table}

\begin{table}[ht]
\caption{Comparing the proposed model performance with existing studies}
\label{existstudies}
\begin{tabular*}{\textwidth}{
p{2.1cm}|
p{1.4cm}|
p{2cm}|
>{\centering\arraybackslash}p{1.6cm}
}
\cline{1-4}
Reference     & Model     & Dataset & Accuracy (\%) \\ \cline{1-4}
\citeauthor{bib5} \cite{bib5} & Res-Net50 & \multirow{2}{*}{Eyes-defy-anemia}   & 97.4     \\ \cline{1-2} \cline{4-4} 
\textbf{Proposed}   & \textbf{YOLOv9}    &        & \textbf{98.2}  \\  \cline{1-4} 
\end{tabular*}
\end{table}

\section{Limitations and Future Works} \label{SEC: limF}
While results are promising, challenges like variable lighting, skin tones, and device heterogeneity remain the limitations of the proposed work. The future can be focused on (1) integrating multimodal data (e.g., symptoms, clinical history) for improved accuracy, (2) optimizing the model for diverse 
%\vspace{-22pt}
demographic groups, and (3) deploying the system in real-time diagnostic platforms to enhance global healthcare accessibility. 
%\vspace{1pt}
\section{Conclusion}\label{sec:con}

This study proposed a non-invasive anemia detection method using improved YOLOv9 to analyze palpebral conjunctiva images. A custom-labeled dataset of palpebral conjunctiva was prepared, incorporating extensive preprocessing and augmentation techniques to enhance model robustness. The proposed model achieved approximately 99\% accuracy, an mAP@50 of 0.995, and an F1-score of 1.00, demonstrates high precision in detecting conjunctival pallor, offering a reliable tool for early anemia screening—particularly beneficial in low-resource or remote settings by reducing dependence on lab tests. 

\section*{Acknowledgment}
The authors express their sincere gratitude to the Ubiquitous, Cloud, and Human-Computer Interaction (UCH) Research Group, Department of Computer Science, American International University-Bangladesh for supporting this research.

\bibliographystyle{IEEEtranN}
\bibliography{refs}
\balance

\end{document}
