<h1 align="center">
  gdown
</h1>

<h4 align="center">
  Download a large file from Google Drive.
</h4>

<div align="center">
  <a href="https://pypi.python.org/pypi/gdown"><img src="https://img.shields.io/pypi/v/gdown.svg"></a>
  <a href="https://pypi.org/project/gdown"><img src="https://img.shields.io/pypi/pyversions/gdown.svg"></a>
  <a href="https://github.com/wkentaro/gdown/actions"><img src="https://github.com/wkentaro/gdown/workflows/ci/badge.svg"></a>
</div>

<div align="center">
  <img src=".readme/cli.png" width="90%">
  <img src=".readme/python.png" width="90%">
</div>

<br/>


## Description

Download a large file from Google Drive.  
If you use curl/wget, it fails with a large file because of
the security warning from Google Drive.
Supports downloading from Google Drive folders (max 50 files per folder).


## Installation

```bash
pip install gdown

# to upgrade
# pip install --upgrade gdown
```


## Usage

### From Command Line

```bash
$ gdown --help
usage: gdown [-h] [-V] [-O OUTPUT] [-q] [--fuzzy] [--id]  [--proxy PROXY]
             [--speed SPEED] [--no-cookies] [--no-check-certificate]
             [--continue] [--folder]
             url_or_id
...

$ # a large file (~500MB)
$ gdown https://drive.google.com/uc?id=1l_5RK28JRL19wpT22B-DY9We3TVXnnQQ
$ # gdown --id 1l_5RK28JRL19wpT22B-DY9We3TVXnnQQ
$ md5sum fcn8s_from_caffe.npz
256c2a8235c1c65e62e48d3284fbd384

$ # a small file
$ gdown https://drive.google.com/uc?id=0B9P1L--7Wd2vU3VUVlFnbTgtS2c
$ cat spam.txt
spam

$ # download with fuzzy extraction of a file ID
$ gdown --fuzzy 'https://drive.google.com/file/d/0B9P1L--7Wd2vU3VUVlFnbTgtS2c/view?usp=sharing&resourcekey=0-WWs_XOSctfaY_0-sJBKRSQ'
$ cat spam.txt
spam

$ # --fuzzy option also works with Microsoft Powerpoint files
$ gdown --fuzzy "https://docs.google.com/presentation/d/15umvZKlsJ3094HNg5S4vJsIhxcFlyTeK/edit?usp=sharing&ouid=117512221203072002113&rtpof=true&sd=true"

$ # a folder
$ gdown https://drive.google.com/drive/folders/1ivUsJd88C8rl4UpqpxIcdI5YLmRD0Mfj -O /tmp/folder --folder

$ # as an alternative to curl/wget
$ gdown https://httpbin.org/ip -O ip.json
$ cat ip.json
{
  "origin": "126.169.213.247"
}

$ # write stdout and pipe to extract
$ gdown https://github.com/wkentaro/gdown/archive/refs/tags/v4.0.0.tar.gz -O - --quiet | tar zxvf -
$ ls gdown-4.0.0
```

### From Python

```python
import gdown

url = 'https://drive.google.com/uc?id=0B9P1L--7Wd2vNm9zMTJWOGxobkU'
output = '20150428_collected_images.tgz'
gdown.download(url, output, quiet=False)

md5 = 'fa837a88f0c40c513d975104edf3da17'
gdown.cached_download(url, output, md5=md5, postprocess=gdown.extractall)

url = 'https://drive.google.com/drive/folders/1ivUsJd88C8rl4UpqpxIcdI5YLmRD0Mfj'
gdown.download_folder(url, quiet=True, no_cookies=True)
```


## License

See [LICENSE](LICENSE).
