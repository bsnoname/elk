Bài viết này chia sẻ cài đặt ELK bằng dockerfile tất cả từ local.
# Cài đặt ELK trên Docker localhost sử dụng dockerfile.

# Dowload 4 file nén và 1 file images nền tảng từ internet về yêu cầu chọn bản TAR.GZ linux 64-bit
# File images nền tảng các bạn dowload về https://hub.docker.com/_/centos với tên file là: centos:7. có thể pull về rồi đưa vào images: Các bạn tự đọc đoạn này để hiểu cách backup và deploy 1 images mới vào docker.
  
  
  # 1: Dowload elasticsearch.tar.gz
  Link Dowload:https://www.elastic.co/downloads/elasticsearch
  # 2: kibana.tar.gz
  Link Dowload https://www.elastic.co/downloads/kibana
  # 3: logstash.tar.gz
  Link Dowload:https://www.elastic.co/downloads/logstash
  # 4: jdk-11.0.6.tar.gz
  Link Dowload:https://www.oracle.com/java/technologies/javase-jdk11-downloads.html

# Tất cả file nén đã dowload ở trên các bạn đưa vào 1 thư mục và đổi tên như thế này
[root@bsnoname elk]# ls
config  Dockerfile  elasticsearch.tar.gz  jdk-11.0.6.tar.gz  kibana.tar.gz  logstash.tar.gz

# Chạy Dockerfile để build imgaes. Lưu ý : Dockerfile của bạn hiện đang nằm trong Dockerfile tôi để ở trên các bạn phải dowload về và đưa vào cùng 1 thư mục
  # Xây dựng images elasticsearch
[root@bsnoname elk]#docker build -t elasticsearch:7.6.1 -f Dockerfile/elasticsearch .
  # Xây dựng images kibana
[root@bsnoname elk]#docker build -t kibana:7.6.1 -f Dockerfile/kibana .
  # Xây dựng images logstash
[root@bsnoname elk]#docker build -t logstash:7.6.1 -f Dockerfile/logstash .

# Sau khi xây dựng xong các image ở trên các bác run images đã buil thành container
  # Chạy container elasticsearch
[root@bsnoname elk]#docker run -d -p 9200:9200 -p 9300:9300 elasticsearch:7.6.1

http//:Địa chỉ ip:9200 để xem kết quả

  # Chạy container kibana
[root@bsnoname elk]#docker run -d -p 5601:5601 kibana:7.6.1

http://Địa chỉ IP:5601/

# Chạy container logstash
[root@bsnoname elk]#docker run -d -p 5504:5504 logstash:7.6.1

Để kiểm tra các bạn có thể đăng nhập vào hẳn container để xem kết quả
