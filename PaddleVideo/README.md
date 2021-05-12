## Model list

| Field | Model | Config | Dataset | Metrics | ACC% | Download |
| :--------------- | :--------: | :------------: | :------------: | :------------: | :------------: | :------------: |
| action recgonition | [ppTSM](./recognition/pp-tsm.md) | [pptsm_k400.yaml](../../../configs/recognition/tsm/pptsm_k400.yaml) | [Kinetics-400](../dataset/k400.md) | Top-1 | 73.5 | [ppTSM.pdparams](https://videotag.bj.bcebos.com/PaddleVideo/ppTSM/ppTSM.pdparams) |
| action recgonition | [SlowFast](./recognition/slowfast.md) | [slowfast_multigrid.yaml](../../../configs/recognition/slowfast/slowfast_multigrid.yaml) | [Kinetics-400](../dataset/k400.md) | Top-1 | 75.84 | [SlowFast.pdparams](https://videotag.bj.bcebos.com/PaddleVideo/SlowFast/SlowFast_8*8.pdparams) |
| action recgonition | [TSM](./recognition/tsm.md) | [tsm.yaml](../../../configs/recognition/tsm/tsm.yaml)  | [Kinetics-400](../dataset/k400.md) | Top-1 | 70.86 | [TSM.pdparams](https://videotag.bj.bcebos.com/PaddleVideo/TSM/TSM.pdparams) |
| action recgonition | [TSN](./recognition/tsn.md) | [tsn.yaml](../../../configs/recognition/tsn/tsn.yaml) | [Kinetics-400](../dataset/k400.md) | Top-1 | 67.0 | TODO |
| action recgonition | [Attention LSTM](./recognition/attention_lstm.md) | [attention_lstm.yaml](../../../configs/recognition/attention_lstm/attention_lstm.yaml) | [Youtube-8M](../dataset/youtube8m.md) | Hit@1 | 89.0 | [AttentionLstm.pdparams](https://videotag.bj.bcebos.com/PaddleVideo/AttentionLstm/AttentionLstm.pdparams) |
| action detection | [BMN](./localization/bmn.md) | [bmn.yaml](../../../configs/localization/bmn.yaml) | [ActivityNet](../dataset/ActivityNet.md) |  AUC | 67.0 | [BMN.pdparams](https://videotag.bj.bcebos.com/PaddleVideo/BMN/BMN.pdparams) 
