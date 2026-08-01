\section{Introduction}
Anemia continues to pose a critical public health concern worldwide, silently affecting countless individuals' health, growth, and productivity. It is defined by a reduced concentration of hemoglobin or a lower number of red blood cells, impairing the blood’s ability to carry oxygen throughout the body \cite{bib1, 7320922}. According to the WHO, anemia is the most common blood disorder, affecting 1.9 billion people worldwide, particularly children under five and women of reproductive age (15–49) \cite{WHO}. Symptoms include fatigue, dizziness, and pale skin, with severe cases leading to cognitive and immune impairments \cite{inbook}. Low- and middle-income countries bear the heaviest burden, with 40\% of preschool children in Africa and South Asia affected. Without intervention, global cases could exceed 700 million by 2050 \cite{bib3, 11013964}. 

Traditional diagnostic methods rely on blood tests and laboratory analysis, which, although accurate, are often invasive, time-consuming, and impractical in resource-limited or rural settings due to the need for sterile equipment, trained personnel, and centralized testing facilities. The common practice for clinicians is to visually inspect the conjunctiva, tongue, nailbeds, and palms to check for pallor, but this is only accurate to a certain extent. This creates a critical need for alternative screening approaches that are affordable, scalable, and easy to deploy, especially in regions lacking access to modern healthcare infrastructure \cite{10534530}.
 
Recent advances in artificial intelligence (AI) and computer vision offer promising results to overcome these challenges. In particular, deep learning models have demonstrated significant potential in medical imaging tasks, enabling automatic analysis with high accuracy and minimal manual effort. The human eye, specifically the paleness of the conjunctiva, has long been used by clinicians as a visual indicator of anemia. Leveraging this physiological cue, computer vision models can be trained to detect anemia-related features in conjunctival images. 

The key contributions of this study are as follows:
\begin{enumerate}
    \item Proposed a deep learning based application for detecting anemia signs from eye conjunctiva images using improved YOLOv9.
    \item Replaced AConv with standard Conv in layers 3, 5, and 9 of the backbone and layer 19 of the neck, reducing layers and parameters. This led to improved inference speed compared to the default YOLOv9s. 
    \item Compared the proposed YOLOv9 model performance with YOLOv8 through YOLOv12 and achieved the highest F1-score of 1.00 and mAP@50 of 0.995, supporting real-time anemia detection. 
\end{enumerate}

The remainder of this paper is organized as follows. Section \ref{sec:RW} reviews prior work on non-invasive anemia detection. Section \ref{sec:PS} details the proposed method, including data collection, preprocessing, and augmentation. Section \ref{sec:ERD} analyzes model performance. Section \ref{SEC: limF} discusses limitations and future work.
Finally, Section \ref{sec:con} concludes the study. 
