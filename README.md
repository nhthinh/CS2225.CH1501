<h1 align="center"> Ứng  dụng tạo ảnh thẻ </h1>

<p align="center">
<a href="https://colab.research.google.com/drive/1ls3jcpKYQfnautkWTKq26-nWK0nX_eHk?usp=sharing"><img  src="https://colab.research.google.com/assets/colab-badge.svg"></a>
</p>


<p align="center">
  <a href="#demo-on-google-colab">Google Colab Demo</a> |
  <a href="#giới-thiệu">Giới thiệu</a> |
  <a href="#phương-pháp-thực-hiện">Phương pháp thực hiện</a> |
  <a href="#bài-toán-segmentation">Bài toán Segmentation </a> |
  <a href="#unet-model">UNET Model</a> |
  <a href="#residual-u-blocks">ReSidual U-Blocks</a> |
  <a href="#u2net-model">U2NET Model</a> | 
  <a href="#dữ-liệu">Dữ liệu</a> |
  <a href="#phương-pháp-đánh-giá">Phương pháp đánh giá</a> | 
  <a href="#liên-hệ">Liên hệ</a>


</p>


### Demo on Google Colab

Yêu cầu khi chạy bước 7 (crop face)
- cần upload model  u2net_portrait.pth từ link  https://drive.google.com/file/d/1IG3HdpcRiDoWNookbncQjeaPN28t90yW/view?usp=sharing và bỏ vào thư mục model. Do file này quá lớn nên không upload được vào github

<p align="justify"> Dành cho các bạn không có môi trường GPUs hoặc là các bạn muốn kiểm thử đơn giản thông qua online, bạn có thể thử phiên bản <a href="https://colab.research.google.com/drive/1ls3jcpKYQfnautkWTKq26-nWK0nX_eHk?usp=sharing">Google Colab</a> để tạo ra kết quả dễ dàng.</p>
Live Demo here in Google colab Link 
<a href="https://colab.research.google.com/drive/1ls3jcpKYQfnautkWTKq26-nWK0nX_eHk?usp=sharing"><img  src="https://colab.research.google.com/assets/colab-badge.svg"></a>

Các bước đã chạy test: https://github.com/nhthinh/CS2225.CH1501/blob/master/PassportMaker_Nhom8.ipynb

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
<br>
<br>
<h1> Loại bài toàn Machine learning </h1>

## Bài toán Segmentation
<p>Tên của lớp bài toán là Image Segmentation có nghĩa là phân khúc hình ảnh, hàm ý rằng bài toán sẽ phân chia một hình ảnh thành nhiều vùng ảnh khác nhau.</p> 
<p>Image Segmentation cũng có chung mục tiêu như object detection là phát hiện ra vùng ảnh chứa vật thể và gán nhãn phù hợp cho chúng. Tuy nhiên tiêu chuẩn về độ chính xác của Image Segmentation ở mức cao hơn so với Object Detection khi nó yêu cầu nhãn dự báo đúng tới từng pixel</p>
</p>Ví dụ Image Segmentation: </p>
<img style="width:255px"  src="docs\images\u2netp_result.png" >
<br/>
<br/>

## UNET Model
* Không sử dụng fully connected do đó cóthể chấp nhận inputvới kích thước bất kì
* Padding method giúp phân đoạn hình ảnh hoàntoàn mà không bị hạn chế bởi dung lượng bộ nhớ GPU.

<img style=""  src="docs\images\Unet_model.png">

## ReSidual U-Blocks
* Được thiết kế nhằm biến đổi các đối tượng x(H x W x Cin) thành các feature map F1(x) với C_out trích xuất local features 
* Nhúng F1(x) vào U-Net tạo liên kết các local features và multi-scale features F1(x) + U(F1(x).

<img style=""  src="docs\images\Residual_U-Blocks.png">


## U2NET Model
* Không sử dụng pre-trained backbones
* Với cấu trúc Encoder-Decoder với mỗi khối là một RSU-block được nhúng U-Net modules nhằm khai thác multi-scale và multi-level features

<img src="docs\images\U2NETPRmodel.png" >


## Dữ Liệu

* Data-train: DUTS-TR là một phần của tập dữ liệu DUTS, có 10553 ảnh. Một tập dữ liệu thường dùng để SOD.
http://saliencydetection.net/duts/download/DUTS-TR.zip

* Data-test: DUT-OMRON có 5168 ảnh có chứa 1 hoặc 2 đối tượng; và ECSSD có 1000 ảnh phức tạp chứa các đối tượng lớn trong ảnh.
http://saliencydetection.net/dut-omron/download/DUT-OMRON-image.zip
https://www.cse.cuhk.edu.hk/leojia/projects/hsaliency/data/ECSSD/images.zip


## Phương pháp đánh giá
<img src="docs\images\pp_danh_gia.png" >

## Liên hệ

* Nguyễn Hoàng Thịnh (thinhnh.15@grad.uit.edu.vn)

* Nguyễn Quan Duy Tùng (tungnqd.15@grad.uit.edu.vn)
* Nguyễn Thanh Phong (phongnt.15@grad.uit.edu.vn)



