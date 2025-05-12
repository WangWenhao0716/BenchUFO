# BenchUFO
![image](https://github.com/WangWenhao0716/BenchUFO/blob/main/bench.png)
The official implementation for **BenchUFO**, which evaluates text-to-video models’ performance on user-focused topics. The benchmark is proposed in our paper [**VideoUFO: A Million-Scale User-Focused Dataset
for Text-to-Video Generation**](https://arxiv.org/abs/2503.01739).

## Results
Currently, we support **16** recent text-to-video models and observe that they do not consistently perform well across all user-focused topics.

<table align="center" border="1" cellspacing="0" cellpadding="6">
  <thead>
    <tr style="background-color: #dddddd; text-align: center;">
      <th>Models</th>
      <th>Low 10</th>
      <th>Low 50</th>
      <th>Top 50</th>
      <th>Top 10</th>
      <th>Link</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Mira</td><td>0.236</td><td>0.282</td><td>0.508</td><td>0.550</td><td><a href="https://github.com/mira-space/Mira">[Link]</a></td>
    </tr>
    <tr>
      <td>Show-1</td><td>0.266</td><td>0.303</td><td>0.524</td><td>0.564</td><td><a href="https://github.com/showlab/Show-1">[Link]</a></td>
    </tr>
    <tr>
      <td>LTX-Video</td><td>0.268</td><td>0.310</td><td>0.532</td><td>0.574</td><td><a href="https://github.com/Lightricks/LTX-Video">[Link]</a></td>
    </tr>
    <tr>
      <td>Open-Sora-Plan</td><td>0.314</td><td>0.361</td><td>0.559</td><td>0.598</td><td><a href="https://github.com/PKU-YuanGroup/Open-Sora-Plan">[Link]</a></td>
    </tr>
    <tr>
      <td>TF-T2V</td><td>0.316</td><td>0.359</td><td>0.560</td><td>0.595</td><td><a href="https://github.com/ali-vilab/VGen">[Link]</a></td>
    </tr>
    <tr>
      <td>Mochi-1</td><td>0.323</td><td>0.367</td><td>0.580</td><td>0.616</td><td><a href="https://github.com/genmoai/mochi">[Link]</a></td>
    </tr>
    <tr>
      <td>HiGen</td><td>0.352</td><td>0.394</td><td>0.589</td><td>0.625</td><td><a href="https://github.com/ali-vilab/VGen">[Link]</a></td>
    </tr>
    <tr>
      <td>Open-Sora</td><td>0.363</td><td>0.409</td><td>0.601</td><td>0.639</td><td><a href="https://github.com/hpcaitech/Open-Sora">[Link]</a></td>
    </tr>
    <tr>
      <td>Pika</td><td>0.365</td><td>0.404</td><td>0.583</td><td>0.619</td><td><a href="https://pika.art/about">[Link]</a></td>
    </tr>
    <tr>
      <td>RepVideo</td><td>0.368</td><td>0.402</td><td>0.589</td><td>0.619</td><td><a href="https://github.com/Vchitect/RepVideo">[Link]</a></td>
    </tr>
    <tr>
      <td>T2V-Zero</td><td>0.375</td><td>0.410</td><td>0.586</td><td>0.616</td><td><a href="https://github.com/Picsart-AI-Research/Text2Video-Zero">[Link]</a></td>
    </tr>
    <tr>
      <td>CogVideoX</td><td>0.383</td><td>0.419</td><td>0.601</td><td>0.629</td><td><a href="https://github.com/THUDM/CogVideo">[Link]</a></td>
    </tr>
    <tr>
      <td>Latte-1</td><td>0.384</td><td>0.421</td><td>0.592</td><td>0.636</td><td><a href="https://github.com/Vchitect/Latte">[Link]</a></td>
    </tr>
    <tr>
      <td>HunyuanVideo</td><td>0.388</td><td>0.427</td><td><u>0.612</u></td><td>0.645</td><td><a href="https://github.com/Tencent/HunyuanVideo">[Link]</a></td>
    </tr>
    <tr>
      <td>LaVie</td><td>0.399</td><td>0.426</td><td>0.595</td><td>0.632</td><td><a href="https://github.com/Vchitect/LaVie">[Link]</a></td>
    </tr>
    <tr>
      <td>Pyramidal</td><td>0.400</td><td>0.433</td><td>0.606</td><td><u>0.647</u></td><td><a href="https://github.com/jy0205/Pyramid-Flow">[Link]</a></td>
    </tr>
  </tbody>
</table>

## Pipeline
Here, we give an example of calculating the score (text similarity) for a given prompt. We take the prompt *"kid pretending to be an astronaut under the moon lit sky Painted by Van Gogh"* and [HunyuanVideo](https://github.com/Tencent/HunyuanVideo) as an example. The full prompt list can be downloaded from [prompts]().

### Step 1: Video Generation.
Input the prompt to a text-to-video model to generate a video. Please prepare the environment and download the text-to-video model according to each repository.
 <td><img src="hunyuan.gif"> </td>

### Step 2: Captioning.
We use a multimodal large language model (here, we choose [QWen2-VL-7B](https://huggingface.co/Qwen/Qwen2-VL-7B-Instruct)) to understand and describe the generated video. Please prepare the environment and download the multimodal large language model according to that repository.

**Input:** (1) The prompt for describing videos: `Please describe the content of this video in as much detail as possible, including the objects, scenery, animals, characters, and camera movements within the video. Do not include \n in your response. Start the description with the video content directly. Describe the content of the video and the changes that occur, in chronological order.`; and (2) the generated video (in `MP4` format).

**Output:** `The video depicts an astronaut standing on a grassy hill under a bright, full moon. The astronaut is wearing a white spacesuit with a gold visor and a backpack. The scene is set against a starry night sky with a large, glowing moon in the background. The landscape features rolling hills and a few scattered trees. The astronaut appears to be in a relaxed posture, with one arm slightly raised. The video captures the astronaut's movements as they step forward, with the left foot leading and the right arm swinging forward. The background remains static, with the moon and stars providing a serene and otherworldly atmosphere. The overall mood of the video is peaceful and contemplative, highlighting the astronaut's solitary presence in a vast, open space.`

### Step 3: Calculating Similarity.
Finally, we calculate the text similarity between the input prompt and the output description.

Preparing the environment:
```python
conda create -n sim python=3.9
pip install sentence-transformers
```
Embedding and calculating similarity:
```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer("sentence-transformers/all-MiniLM-L6-v2")
```

## Curators
BenchUFO is created by [Wenhao Wang](https://wangwenhao0716.github.io/) and Professor [Yi Yang](https://scholar.google.com/citations?user=RMSuNFwAAAAJ&hl=zh-CN).

## License
The code for BenchUFO is released under the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/deed.en). The benchmarked video generation models and the multimodal large language model used have their own licenses. 

## Citation
```
@article{wang2025videoufo,
  title={VideoUFO: A Million-Scale User-Focused Dataset for Text-to-Video Generation},
  author={Wang, Wenhao and Yang, Yi},
  journal={arXiv preprint arXiv:2503.01739},
  year={2025}
}
```
## Contact
If you have any questions, feel free to contact Wenhao Wang (wangwenhao0716@gmail.com).
