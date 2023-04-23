# Java の SDK で AWS S3 バケットを作成して画像を保存する方法

この記事では、Java の SDK を使用して AWS S3 バケットを作成し、画像を保存する方法について解説します。AWS S3 は、Amazon Web Services（AWS）が提供するオブジェクトストレージサービスで、インターネット上でデータを安全かつ効率的に保存・取得することができます。

## 前提条件

以下の前提条件が整っていることを確認してください。

1. AWS アカウントが作成済みであること
2. AWS CLI がインストール済みであること
3. AWS SDK for Java がインストール済みであること

## 手順

### 1. AWS SDK for Java をインストールする

まずは、AWS SDK for Java をインストールしましょう。こちらの公式ドキュメントを参照して、最新の SDK をインストールしてください。[https://aws.amazon.com/jp/sdk-for-java/](https://aws.amazon.com/jp/sdk-for-java/)

### 2. S3 バケットを作成する

次に、S3 バケットを作成します。以下のコードを実行して、新しい S3 バケットを作成してください。

```java

import com.amazonaws.AmazonServiceException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.CreateBucketRequest;
import com.amazonaws.services.s3.model.Region;l

public class CreateBucket {
    public static void main(String[] args) {
        final String bucket_name = "my-bucket";
        final AmazonS3 s3 = AmazonS3ClientBuilder.defaultClient();

        try {
            s3.createBucket(new CreateBucketRequest(bucket_name, Region.US_West));
            System.out.println("バケット " + bucket_name + " が作成されました。");
        } catch (AmazonServiceException e) {
            System.err.println(e.getErrorMessage());
            System.exit(1);
        }
    }
}
```

### 3. 画像ファイルを S3 バケットにアップロードする

最後に、画像ファイルを S3 バケットにアップロードします。以下のコードを実行して、画像ファイルをアップロードしてください。

```java

import com.amazonaws.AmazonServiceException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.PutObjectRequest;

import java.io.File;

public class UploadObject {
    public static void main(String[] args) {
        final String bucket_name = "my-bucket";
        final String file_path = "path/to/your/image.jpg";
        final String key_name = "image.jpg";

        final AmazonS3 s3 = AmazonS3ClientBuilder.defaultClient();
        try {
            s3.putObject(new PutObjectRequest(bucket_name, key_name, new File(file_path)));
            System.out.println("画像ファイル " + file_path + " がS3バケット " + bucket_name + " にアップロードされました。");
            } catch (AmazonServiceException e) {
            System.err.println(e.getErrorMessage());
            System.exit(1);
            }
    }
}
```

これで、Java の SDK を使って AWS S3 バケットを作成し、画像を保存する方法が完了しました。

## まとめ

この記事では、Java の SDK を使用して AWS S3 バケットを作成し、画像をアップロードする方法について解説しました。具体的な手順は以下の通りです。

1. AWS SDK for Java をインストールする
2. S3 バケットを作成する
3. 画像ファイルを S3 バケットにアップロードする
