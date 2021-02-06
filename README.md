<h1 align="center"> Ứng  dụng tạo ảnh thẻ </h1>

<p align="center">
<a href="https://colab.research.google.com/drive/1ls3jcpKYQfnautkWTKq26-nWK0nX_eHk?usp=sharing"><img  src="https://colab.research.google.com/assets/colab-badge.svg"></a>
</p>


<p align="center">
  <a href="#demo-on-google-colab">Google Colab Demo</a> |
  <a href="#giới-thiệu">Giới thiệu</a> |
  <a href="#phương-pháp-thực-hiện">Phương pháp thực hiện</a> |
  <a href="#u2net-model">U2NET Model</a> 
</p>


### Demo on Google Colab

<p align="justify"> Dành cho các bạn không có môi trường GPUs hoặc là các bạn muốn kiểm thử đơn giản thông qua online, bạn có thể thử phiên bản <a href="https://colab.research.google.com/drive/1ls3jcpKYQfnautkWTKq26-nWK0nX_eHk?usp=sharing">Google Colab</a> để tạo ra kết quả dễ dàng.</p>

<a href="https://colab.research.google.com/drive/1ls3jcpKYQfnautkWTKq26-nWK0nX_eHk?usp=sharing"><img  src="https://colab.research.google.com/assets/colab-badge.svg"></a>


## Giới thiệu

<p align="justify"> Ứng dụng tạo ảnh thẻ giúp cá nhân chúng ta có thể biến 1 tấm ảnh bình thường rõ mặt thành hình ảnh thẻ chân dung theo chuẩn yêu cầu khi làm ảnh thẻ nhân viên, CMND hoặc hộ chiếu.
Với đầu vào là 1 ảnh bình thường : </p>
<img src="docs\images\anhinput.jpg">
<p>Kết quả trả về hình thẻ chân dung</p>
<img src="docs\images\anhoutput.png">


## Phương Pháp Thực Hiện

* Salient Object Detection (phát hiện đối tượng nổi bật) (SOD) nhằm mục đích bóc tách (segmentation) các đối tượng trong hình ảnh.
* Sử dụng Deep Convolutional Neural Networks (CNN), Fully Convolutional Networks (FCN) nhằm segmentation hình ảnh
* SOD được cải thiện so với trích xuất bởi backbones, chẳng hạn như Alexnet, VGG, ResNet, DenseNet,... vì mục đích backbones ban đầu được thiết kế để phân loại, trích xuất tính năng đại diện để định danh hơn là segmentation toàn bộ đối tượng


## U2NET Model
<img src="docs\images\U2NETPRmodel.png" >

<p>Kết quả khi sử dụng u2net Model để bóc tách đối tượng: </p>

<img src="docs\images\u2netp_result.png" >





