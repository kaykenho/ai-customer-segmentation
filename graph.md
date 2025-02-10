```mermaid

flowchart TB
    subgraph Data["1. Data Preprocessing"]
        direction TB
        RawData["Raw Customer Data"]
        Clean["Data Cleaning"]
        FeatEng["Feature Engineering"]
        Split["Train-Test Split"]
        
        RawData --> Clean
        Clean --> |"Remove duplicates\nHandle missing values"| FeatEng
        FeatEng --> |"One-Hot Encoding\nStandardScaling"| Split
        Split --> |"70% Training"| TrainData["Training Data"]
        Split --> |"30% Testing"| TestData["Testing Data"]
    end

    subgraph Classification["2. Classification Models"]
        direction TB
        RF["Random Forest Classifier"]
        XGB["XGBoost Classifier"]
        GridCV["GridSearchCV\nHyperparameter Tuning"]
        
        RF --> GridCV
        XGB --> GridCV
        GridCV --> |"Optimal Parameters"| ClassOut["Classification Output\n- Delinquency Prediction"]
    end

    subgraph Segmentation["3. Customer Segmentation"]
        direction TB
        KMeans["K-means Clustering"]
        Elbow["Elbow Method\nOptimal Clusters"]
        Quality["Silhouette Score\nCluster Quality"]
        
        KMeans --> Elbow
        Elbow --> Quality
        Quality --> SegOut["Segmentation Output\n- Risk Categories"]
    end

    subgraph RL["4. Reinforcement Learning"]
        direction TB
        QLearning["Q-Learning Agent"]
        State["State Space\n(Risk Levels)"]
        Action["Action Space\n(Approve/Deny)"]
        Reward["Reward Matrix"]
        
        State --> QLearning
        Action --> QLearning
        Reward --> QLearning
        QLearning --> RLOut["Optimized Credit\nApproval Policies"]
    end

    subgraph Eval["5. Model Evaluation"]
        direction TB
        ClassEval["Classification Metrics\n- Accuracy\n- AUC-ROC\n- F1-Score\n- Confusion Matrix"]
        SegEval["Segmentation Metrics\n- Silhouette Score\n- Elbow Method"]
        RLEval["RL Metrics\n- Cumulative Return"]
    end

    subgraph Deploy["6. Deployment & Monitoring"]
        direction TB
        Prod["Production Integration"]
        Monitor["Continuous Monitoring"]
        Feedback["Feedback Loop"]
        
        Prod --> Monitor
        Monitor --> Feedback
        Feedback --> |"Model Retraining"| Prod
    end

    TrainData --> Classification
    TestData --> Classification
    TrainData --> Segmentation
    ClassOut --> Eval
    SegOut --> Eval
    RLOut --> Eval
    Eval --> Deploy
