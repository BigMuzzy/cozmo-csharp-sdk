```mermaid
stateDiagram-v2
        state IHT_Session {
                IHT_Setup
                IHT_Running
                IHT_Paused
                IHT_Completed
        }
        state IHT_Running {
                HypoxicInterval
                NormoxicInterval
        }
        Idle --> IHT_Session : StartIHT
        IHT_Session --> Idle : Complete
        IHT_Session --> Emergency_Shutdown : BiofeedbackAlert
        IHT_Setup --> IHT_Running : Start
        IHT_Running --> IHT_Paused : Pause
        HypoxicInterval --> NormoxicInterval : IntervalCompleted
        HypoxicInterval --> IHT_Paused : BiofeedbackAlert
        NormoxicInterval --> HypoxicInterval : IntervalCompleted
        NormoxicInterval --> IHT_Completed : AllCyclesCompleted
        IHT_Paused --> IHT_Running : Resume
        IHT_Completed --> Idle : Complete
[*] --> Idle
