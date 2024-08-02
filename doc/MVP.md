## MVP. Config CI process for your App by ArgoCD and testing

### Create new App
Use yaml config  bellow
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: demo
spec:
  destination:
    name: ''
    namespace: demo
    server: 'https://kubernetes.default.svc'
  source:
    path: helm
    repoURL: 'https://github.com/den-vasyliev/go-demo-app'
    targetRevision: HEAD
  sources: []
  project: default
  syncPolicy:
    syncOptions:
      - CreateNamespace=true
```

### Enable automated sync policy in Details tab your created App

![Demo GIF](https://raw.githubusercontent.com/brokerUA/devops101-w4-m4-t4/main/doc/resources/mvp_01__argocd.gif)

## Test your App

### Port forwarding
```bash
kubectl port-forward -n demo svc/ambassador 8088:80
```

### Get current version
```bash
curl localhost:8088
```
ex.: `k8sdiy-api:599e1af`

### Download test image
```bash
wget -O /tmp/test.png https://user-images.githubusercontent.com/25306803/43103633-a5d61dc4-8e83-11e8-9f0e-7ccdbee01eb6.png
```

### Convert to ASCII art
```bash
curl -F 'image=@/tmp/test.png' localhost:8088/img/
```
ex.:

                            ,:;1ttffffft1i:,.                                                   
                       .;tLG88@@@@@@@@@@@@880Cfi,                                               
                    ,1C0@@@@@88888888888888@@@@@8Gt:                                            
                  ;L8@@@888@@8888888888888888888@@@8C1.                                         
                ;C8@@88@@@88888888888888888888888888@@01.                                       
              ,L8@888@@@888888880000G00088888888888888@@G;                                      
             ;0@888@@@8888888GCLffffffffLLG0888888888888@8t                                     
            18@88@@@8888880CfffffffffffffttfL08888888888888L.                                   
           i8888@i8888888GfffLCCLffffffffffftfC8888888888888L                                   
          ,0888@@8888888GfffffLLfffffffffffffftC88888888888881                                  
        ,,L8888@@8888888LfffffffffffffffffffffftG8888888888880;,                                
       ,000888@@88888880tftttfffffffffffffftttttC888888888888000,                               
       :0G0@88@@888888GLfCCGCLftfffffffftfLCCCLffC8888888888@8G0:                               
       ,0G8888@888880fL0@@@@@@@GffffffffG8@@@@@@0Lf0888888888800,                               
       ,0G8@88@@8888fL@@@C,,;8@@8ffffff0@@@t,,f@@@Lf08888888@8G0,                               
       :000888@@8880t0@@@C,,;8@@@CtfffL@@@@t,,f@@@0tG8888888@800:                               
       ,CCG888@@8888fL@@@@@@@@@@8ffffff0@@@@@@@@@@Ct0888888880GC,                               
          ;8888@@8880fL0@@@@@@@0ffffffffG@@@@@@@8LfG888888888f.                                 
           f@888@@8888GLLCGGCCftfffffffftfLCGGCLfC0888888888G.                                  
            L@888@@88880fttttfffffffffffffftttft0888888888@0:                                   
             f8@88@@8888Lfffffffffffffftffffffff088888888@C,                                    
              i0@@888888LffffffL0CffffLGCfffffff0888888@8f.                                     
               .f8@@888LL:ffffft10@88@8f1ffffffL88888@8C;                                       
                 ,t0@@@LCff:ffffi.,:;:.:fffffffLL8@@8L;                                         
                   .iL0@Gtffffffft;,,:1ffffffffC@8Gt,                                           
                      .:tffffff:ffffffffffffff:f:,                                              
                        ,f:ffffffffffffffffffff:.                                               
                   ,:;itt:ffffffffffffffffffffftt1i:,.                                          
                         tff1tfffffffffffff1fff.                                                
                         tffitfttffffffttffifff.                                                
                         1ff;tf11fffffft1ff;tft                                                 
                         iff,tfiiffffff1iff,tf1                                                 
                         ;ff.tf;ifft1ff1:ff,1fi                                                 
                    .,,;itt; fL:iff;,ff1,ff.,tti;:,.                                            
                    ..,,:;;:iti iff. tft ;t1;:;::,..                                            
                        ..,:::;1ft;  :tf1;;::,..                                                
                          .,,:::,      .,::,,..                                                 
                                                                                                 
