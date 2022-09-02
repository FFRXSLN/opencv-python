[![İndirilenler](http://pepy.tech/badge/opencv-python)](http://pepy.tech/project/opencv-python)

##  OpenCV

Python için önceden oluşturulmuş CPU-only OpenCV paketleri.

CUDA gibi ek modülleri etkinleştirmek için bağlamaları kaynaktan derlemek istiyorsanız manuel derleme bölümünü kontrol edin.

### Kurulum ve Kullanım

1. OpenCV'nin önceki/diğer manuel olarak yüklenmiş (= ``pip`` ile yüklenmemiş) sürümü yüklüyse (örneğin Python'un site-packages kök dizinindeki cv2 modülü), çakışmaları önlemek için kurulumdan önce kaldırın.
2. pip` sürümünüzün güncel olduğundan emin olun (19.3 desteklenen minimum sürümdür): pip install --upgrade pip`. Pip -V` ile sürümü kontrol edin. Örneğin Linux dağıtımları genellikle çok eski `pip` sürümleriyle birlikte gelir ve bu da özellikle `manylinux` formatında beklenmedik sorunlara neden olur.
3. Ortamınız için doğru paketi seçin:

    Dört farklı paket vardır (aşağıdaki 1, 2, 3 ve 4 numaralı seçeneklere bakın) ve **BUNLARDAN SADECE BİRİNİ** SEÇMELİSİNİZ. Aynı ortama birden fazla farklı paket yüklemeyin. Eklenti mimarisi yoktur: tüm paketler aynı ad alanını (`cv2`) kullanır. Aynı ortama birden fazla farklı paket yüklediyseniz, hepsini ``pip uninstall`` ile kaldırın ve yalnızca bir paketi yeniden yükleyin.

    **a.** Standart masaüstü ortamları için paketler (Windows, macOS, neredeyse tüm GNU/Linux dağıtımları)

    - Seçenek 1 - Ana modül paketi: ``pip install opencv-python``
    - Seçenek 2 - Tam paket (hem ana modülleri hem de contrib/extra modüllerini içerir): ``pip install opencv-contrib-python`` ([OpenCV belgeleri](https://docs.opencv.org/master/) adresindeki contrib/extra modülleri listesini kontrol edin)

    **b.** Sunucu (headless) ortamlar için paketler (Docker, bulut ortamları vb. gibi), GUI kütüphane bağımlılıkları yok

    Bu paketler yukarıdaki diğer iki paketten daha küçüktür çünkü herhangi bir GUI işlevi içermezler (Qt / diğer GUI bileşenleri ile derlenmezler). Bu, paketlerin X11 kütüphanelerine ağır bir bağımlılık zincirinden kaçındığı ve sonuç olarak örneğin daha küçük Docker görüntülerine sahip olacağınız anlamına gelir. Eğer `cv2.imshow` ve diğerlerini kullanmıyorsanız veya GUI'nizi oluşturmak için OpenCV'den başka bir paket (PyQt gibi) kullanıyorsanız bu paketleri her zaman kullanmalısınız.

    - Seçenek 3 - Headless ana modül paketi: ``pip install opencv-python-headless``
    - Seçenek 4 - Headless tam paket (hem ana modülleri hem de contrib/extra modüllerini içerir): ``pip install opencv-contrib-python-headless`` ([OpenCV documentation](https://docs.opencv.org/master/) adresinden contrib/extra modules listesini kontrol edin)

4. Paketi içe aktarın:

    ``import cv2``

    Tüm paketler Haar kaskad dosyalarını içerir. ``cv2.data.haarcascades`` veri klasörüne kısayol olarak kullanılabilir. Örneğin:

    ``cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_frontalface_default.xml")``

5. OpenCV belgelerini okuyun](https://docs.opencv.org/master/)

6. Yeni bir sorun açmadan önce aşağıdaki SSS bölümünü okuyun ve halihazırda açık olan diğer sorunlara göz atın.

Sıkça Sorulan Soruları
--------------------------

**S: OpenCV'yi ayrıca yüklemem gerekiyor mu?

C: Hayır, paketler özel tekerlek ikili paketleridir ve zaten statik olarak oluşturulmuş OpenCV ikili dosyalarını içerirler.

**S: Pip kurulumu ``ModuleNotFoundError: 'skbuild'` adında bir modül yok?

OpenCV-python`` 4.3.0.\* sürümünden bu yana, ``manylinux1`` tekerlekleri ``manylinux2014`` tekerlekleri ile değiştirildi. Eğer pip'iniz çok eskiyse, OpenCV'yi elle derlemek için 4.3.0.38'de sunulan yeni kaynak dağıtımını kullanmaya çalışacaktır çünkü ``manylinux2014`` tekerleklerini nasıl kuracağını bilmemektedir. Ancak, ``pyproject.toml`` içindeki derleme bağımlılıklarını anlamadığı için çok eski ``pip`` nedeniyle kaynak derleme de başarısız olacaktır. Yeni ``manylinux2014`` önceden oluşturulmuş tekerlekleri kullanmak için (veya kaynaktan derlemek için), ``pip`` sürümünüz >= 19.3 olmalıdır. Lütfen ``pip`` sürümünü ``pip install --upgrade pip`` ile yükseltin.

**S: Windows'ta içe aktarma başarısız oluyor: ``ImportError: DLL yüklemesi başarısız oldu: Belirtilen modül bulunamadı``?

C: Windows'ta içe aktarma başarısız olursa, [Visual C++ redistributable 2015] (https://www.microsoft.com/en-us/download/details.aspx?id=48145) yüklü olduğundan emin olun. Windows 10'dan daha eski bir Windows sürümü kullanıyorsanız ve en son sistem güncellemeleri yüklü değilse, [Universal C Runtime](https://support.microsoft.com/en-us/help/2999226/update-for-universal-c-runtime-in-windows) da gerekli olabilir.

Windows N ve KN sürümleri OpenCV tarafından gerekli olan Medya Özellik Paketini içermez. Windows N veya KN sürümü kullanıyorsanız, lütfen [Windows Media Feature Pack](https://support.microsoft.com/en-us/help/3145500/media-feature-pack-list-for-windows-n-editions)'i de yükleyin.

If you have Windows Server 2012+, media DLLs are probably missing too; please install the Feature called "Media Foundation" in the Server Manager. Beware, some posts advise to install "Windows Server Essentials Media Pack", but this one requires the "Windows Server Essentials Experience" role, and this role will deeply affect your Windows Server configuration (by enforcing active directory integration etc.); so just installing the "Media Foundation" should be a safer choice.

If the above does not help, check if you are using Anaconda. Old Anaconda versions have a bug which causes the error, see [this issue](https://github.com/opencv/opencv-python/issues/36) for a manual fix.

If you still encounter the error after you have checked all the previous solutions, download [Dependencies](https://github.com/lucasg/Dependencies) and open the ``cv2.pyd`` (located usually at ``C:\Users\username\AppData\Local\Programs\Python\PythonXX\Lib\site-packages\cv2``) file with it to debug missing DLL issues.

**Q: I have some other import errors?**

A: Make sure you have removed old manual installations of OpenCV Python bindings (cv2.so or cv2.pyd in site-packages).

**Q: Function foo() or method bar() returns wrong result, throws exception or crashes interpreter. What should I do?**

A: The repository contains only OpenCV-Python package build scripts, but not OpenCV itself. Python bindings for OpenCV are developed in official OpenCV repository and it's the best place to report issues. Also please check {OpenCV wiki](https://github.com/opencv/opencv/wiki) and [the official OpenCV forum](https://forum.opencv.org/) before file new bugs.

**Q: Why the packages do not include non-free algorithms?**

A: Non-free algorithms such as SURF are not included in these packages because they are patented / non-free and therefore cannot be distributed as built binaries. Note that SIFT is included in the builds due to patent expiration since OpenCV versions 4.3.0 and 3.4.10. See this issue for more info: https://github.com/skvark/opencv-python/issues/126

**Q: Why the package and import are different (opencv-python vs. cv2)?**

A: It's easier for users to understand ``opencv-python`` than ``cv2`` and it makes it easier to find the package with search engines. `cv2` (old interface in old OpenCV versions was named as `cv`) is the name that OpenCV developers chose when they created the binding generators. This is kept as the import name to be consistent with different kind of tutorials around the internet. Changing the import name or behaviour would be also confusing to experienced users who are accustomed to the ``import cv2``.

## Documentation for opencv-python

[![Windows Build Status](https://github.com/opencv/opencv-python/actions/workflows/build_wheels_windows.yml/badge.svg)](https://github.com/opencv/opencv-python/actions/workflows/build_wheels_windows.yml)
[![(Linux Build status)](https://github.com/opencv/opencv-python/actions/workflows/build_wheels_linux.yml/badge.svg)](https://github.com/opencv/opencv-python/actions/workflows/build_wheels_linux.yml)
[![(Mac OS Build status)](https://github.com/opencv/opencv-python/actions/workflows/build_wheels_macos.yml/badge.svg)](https://github.com/opencv/opencv-python/actions/workflows/build_wheels_macos.yml)

The aim of this repository is to provide means to package each new [OpenCV release](https://github.com/opencv/opencv/releases) for the most used Python versions and platforms.

### CI build process

The project is structured like a normal Python package with a standard ``setup.py`` file.
The build process for a single entry in the build matrices is as follows (see for example `.github/workflows/build_wheels_linux.yml` file):

0. In Linux and MacOS build: get OpenCV's optional C dependencies that we compile against

1. Checkout repository and submodules

   -  OpenCV is included as submodule and the version is updated
      manually by maintainers when a new OpenCV release has been made
   -  Contrib modules are also included as a submodule

2. Find OpenCV version from the sources

3. Build OpenCV

   -  tests are disabled, otherwise build time increases too much
   -  there are 4 build matrix entries for each build combination: with and without contrib modules, with and without GUI (headless)
   -  Linux builds run in manylinux Docker containers (CentOS 5)
   -  source distributions are separate entries in the build matrix

4. Rearrange OpenCV's build result, add our custom files and generate wheel

5. Linux and macOS wheels are transformed with auditwheel and delocate, correspondingly

6. Install the generated wheel
7. Test that Python can import the library and run some sanity checks
8. Use twine to upload the generated wheel to PyPI (only in release builds)

Steps 1--4 are handled by ``pip wheel``.

The build can be customized with environment variables. In addition to any variables that OpenCV's build accepts, we recognize:

 ``CI_BUILD``. CI ortamı derleme davranışını taklit etmek için ``1`` olarak ayarlayın. Sadece CI derlemelerinde ``setup.py`` içinde belirli derleme bayraklarını zorlamak için kullanılır. Ne yaptığınızı bilmiyorsanız bunu kullanmayın.
- ENABLE_CONTRIB`` ve ``ENABLE_HEADLESS``. Contrib ve/veya headless sürümünü derlemek için ``1`` olarak ayarlayın
- ``ENABLE_JAVA``, Java istemci yapısını etkinleştirmek için ``1`` olarak ayarlayın.  Bu varsayılan olarak devre dışıdır.
- ``CMAKE_ARGS``. OpenCV'nin CMake çağrısı için ek argümanlar. Bunu özel bir derleme yapmak için kullanabilirsiniz.

CI ortamı dışında manuel derlemeler hakkında daha fazla bilgi için bir sonraki bölüme bakın.

### Manuel derlemeler

Önceden oluşturulmuş tekerleklerde bazı bağımlılıklar etkinleştirilmemişse, özel bir tekerlek oluşturmak için derlemeyi yerel olarak da çalıştırabilirsiniz.

1. Bu depoyu klonlayın: `git clone --recursive https://github.com/opencv/opencv-python.git`
2. ``cd opencv-python``
    - Gerekirse `opencv` ve `opencv_contrib` alt modüllerinde OpenCV'nin başka bir sürümünü kontrol etmek için `git` kullanabilirsiniz
3. Gerekirse özel Cmake bayrakları ekleyin, örneğin: `export CMAKE_ARGS="-DSOME_FLAG=ON -DSOME_OTHER_FLAG=OFF"` (Windows'ta Komut Satırı veya PowerShell'e bağlı olarak ortam değişkenlerini farklı şekilde ayarlamanız gerekir)
4. ENABLE_CONTRIB` ve `ENABLE_HEADLESS` ile oluşturmak istediğiniz paket türünü seçin: örneğin, `opencv-contrib-python` oluşturmak istiyorsanız `export ENABLE_CONTRIB=1`
5. Çalıştır ``pip wheel . --verbose`` komutunu çalıştırın. NOT: En son ``pip`` sürümüne sahip olduğunuzdan emin olun, ``pip wheel`` komutu ``pyproject.toml`` dosyasını desteklemeyen eski ``python setup.py bdist_wheel`` komutunun yerini alır.
    - Bu işlem donanımınıza bağlı olarak 5 dakika ile 2 saat arasında sürebilir
6. Tekerlek dosyası `dist` klasöründe olacak ve bununla dilediğinizi yapabilirsiniz
    - İsteğe bağlı: Linux'ta maksimum taşınabilirlik gerekiyorsa derleme ana bilgisayarı olarak `manylinux` görüntülerinden bazılarını kullanın ve derlemeden sonra tekerlek için `auditwheel` çalıştırın
    - İsteğe bağlı: macOS'ta daha iyi taşınabilirlik için ``delocate`` (``auditwheel`` ile aynı ancak macOS için) kullanın

#### Manuel hata ayıklama derlemeleri

Optimize edilmemiş bir hata ayıklama derlemesinde `opencv-python` derlemek için, normal süreçten biraz sapmanız gerekir.

1. Pip aracılığıyla `scikit-build` ve `numpy` paketlerini yükleyin.
2. python setup.py bdist_wheel --build-type=Debug` komutunu çalıştırın.
3. Oluşturulan tekerlek dosyasını `pip install dist/wheelname.whl` ile `dist/` klasörüne yükleyin.

Derlemenin tüm derleyici komutlarını üretmesini istiyorsanız, aşağıdaki bayrak ve ortam değişkenleri kombinasyonunun Linux üzerinde çalıştığı test edilmiştir:
```
export CMAKE_ARGS='-DCMAKE_VERBOSE_MAKEFILE=ON'
export VERBOSE=1

python3 setup.py bdist_wheel --build-type=Debug
```

Daha fazla tartışma için bu sayıya bakınız: https://github.com/opencv/opencv-python/issues/424

#### Kaynak dağıtımları

OpenCV 4.3.0 sürümünden bu yana, PyPI'da kaynak dağıtımları da sağlanmaktadır. Bu, sisteminizin PyPI'daki tekerleklerden herhangi biriyle uyumlu olmadığı anlamına gelir, ``pip`` OpenCV'yi kaynaklardan oluşturmaya çalışacaktır. PyPI'da kaynak dağıtım olarak bulunmayan bir OpenCV sürümüne ihtiyacınız varsa, lütfen bunun yerine yukarıdaki manuel derleme kılavuzunu izleyin.

Ayrıca ``pip``i tekerlekleri kaynak dağıtımdan oluşturmaya zorlayabilirsiniz. Bazı örnekler:

- ``pip install --no-binary opencv-python opencv-python``
- ``pip install --no-binary :all: opencv-python``

Eğer contrib modüllerine veya headless sürümüne ihtiyacınız varsa, sadece paket adını değiştirin (önceki bölümdeki 4. adım gerekli değildir). Bununla birlikte, herhangi bir ek CMake bayrağı, manuel derleme bölümünün 3. adımında açıklandığı gibi ortam değişkenleri aracılığıyla sağlanabilir. Hiçbiri sağlanmamışsa, OpenCV'nin CMake komut dosyaları uygun bağımlılıkları bulmaya ve etkinleştirmeye çalışacaktır. Headless dağıtımları, tüm olası GUI bağımlılıklarını devre dışı bırakan sabit kodlanmış CMake bayraklarına sahiptir.

Raspberry Pi gibi yavaş sistemlerde tam derleme birkaç saat sürebilir. 8 çekirdekli Ryzen 7 3700X üzerinde derleme yaklaşık 6 dakika sürer.

### Lisanslama

Opencv-python paketi (bu depodaki betikler) MIT lisansı altında mevcuttur.

OpenCV'nin kendisi [Apache 2](https://github.com/opencv/opencv/blob/master/LICENSE) lisansı altında mevcuttur.

Üçüncü taraf paket lisansları [LICENSE-3RD-PARTY.txt](https://github.com/opencv/opencv-python/blob/master/LICENSE-3RD-PARTY.txt) adresindedir.

Tüm tekerlekler [LGPLv2.1](http://www.gnu.org/licenses/old-licenses/lgpl-2.1.html) lisansı altında [FFmpeg](http://ffmpeg.org) ile birlikte gönderilir.

Başlıksız Linux tekerlekleri [LGPLv3](http://www.gnu.org/licenses/lgpl-3.0.html) altında lisanslanan [Qt 5](http://doc.qt.io/qt-5/lgpl.html) ile birlikte gönderilir.

Paketler diğer ikili dosyaları da içerir. Lisansların tam listesi [LICENSE-3RD-PARTY.txt](https://github.com/opencv/opencv-python/blob/master/LICENSE-3RD-PARTY.txt) adresinde bulunabilir.

### Sürüm Oluşturma
``find_version.py`` betiği OpenCV kaynaklarından sürüm bilgilerini arar ve sürüm dizesine bu depoya özgü bir revizyon numarası da ekler. Sürüm bilgisini diğer bazı bayraklara ek olarak ``cv2`` altındaki ``version.py`` dosyasına kaydeder.

### Sürümler

Yeni bir etiket ana dala itildiğinde bir sürüm yapılır ve PyPI'a yüklenir. Bu etiketler paketleri birbirinden ayırır (bu repoda değişiklikler olabilir ancak OpenCV sürümü aynı kalır) ve sırayla artırılmalıdır. Uygulamada, sürüm numaraları şu şekilde görünür:

``cv_major.cv_minor.cv_revision.package_revision`` örneğin ``3.1.0.0``

Ana dal OpenCV ana dal sürümlerini takip eder. 3.4 dalı OpenCV 3.4 hata düzeltme sürümlerini takip eder.

### Geliştirme yapıları

Bu deponun ana dalına yapılan her işlem derlenecektir. Olası derleme eserleri yerel sürüm tanımlayıcılarını kullanır:

``cv_major.cv_minor.cv_revision+git_hash_of_this_repo`` örneğin ``3.1.0+14a8d39``

Bu eserler PyPI'a yüklenemez ve yüklenmeyecektir.

### Manylinux tekerlekleri

Linux tekerlekleri [manylinux2014](https://github.com/pypa/manylinux) kullanılarak oluşturulmuştur. Bu tekerlekler, eski bir glibc sürümüne karşı oluşturulduğundan, çoğu dağıtım (GNU C standart kütüphanesini kullanan) için kutudan çıkar çıkmaz çalışmalıdır.

Varsayılan ``manylinux2014`` görüntüleri bazı OpenCV bağımlılıkları ile genişletilmiştir. Daha fazla bilgi için [Docker folder](https://github.com/skvark/opencv-python/tree/master/docker) adresine bakın.

### Desteklenen Python sürümleri

Python 3.x uyumlu önceden oluşturulmuş tekerlekler, resmi olarak desteklenen Python sürümleri için sağlanmıştır (EOL'de değil):

- 3.6
- 3.7
- 3.8
- 3.9
- 3.10

### Geriye dönük uyumluluk

4.2.0 ve 3.4.9 sürümlerinden başlayarak macOS Travis derleme ortamı XCode 9.4'e güncellendi. Bu değişiklik, 10.13 macOS sürümünden daha eski sürümler için desteği etkin bir şekilde ortadan kaldırdı.

4.3.0 ve 3.4.10 sürümlerinden itibaren Linux derleme ortamı `manylinux1`den `manylinux2014`e güncellendi. Böylece eski Linux dağıtımları için destek kesildi.
