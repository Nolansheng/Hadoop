# 使用Eclipse开发hadoop程序
1. 新建一个Map/Reduce Project
2. 新建一个class
## 3. wordcount 实例
```
import java.io.*;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class wordcount {
	 
	  public static class TokenizerMapper
	       extends Mapper<Object, Text, Text, IntWritable>{
	 
	    private final static IntWritable one = new IntWritable(1);
	    private Text word = new Text();
	 
	    public void map(Object key, Text value, Context context
	                    ) throws IOException, InterruptedException {
	      StringTokenizer itr = new StringTokenizer(value.toString());
	      while (itr.hasMoreTokens()) {
	        word.set(itr.nextToken());
	        context.write(word, one);
	      }
	    }
	  }
	 
	  public static class IntSumReducer
	       extends Reducer<Text,IntWritable,Text,IntWritable> {
	    private IntWritable result = new IntWritable();
	 
	    public void reduce(Text key, Iterable<IntWritable> values,
	                       Context context
	                       ) throws IOException, InterruptedException {
	      int sum = 0;
	      for (IntWritable val : values) {
	        sum += val.get();
	      }
	      result.set(sum);
	      context.write(key, result);
	    }
	  }
	 
	  public static void main(String[] args) throws Exception {
	    Configuration conf = new Configuration();
	    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
	    if (otherArgs.length != 2) {
	      System.err.println("Usage: wordcount <in> <out>");
	      System.exit(2);
	    }
//	    @SuppressWarnings("deprecation")
	Job job = new Job(conf, "word count");
	    job.setJarByClass(wordcount.class);
	    job.setMapperClass(TokenizerMapper.class);
	    job.setCombinerClass(IntSumReducer.class);
	    job.setReducerClass(IntSumReducer.class);
	    job.setOutputKeyClass(Text.class);
	    job.setOutputValueClass(IntWritable.class);
	    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
	    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
	    System.exit(job.waitForCompletion(true) ? 0 : 1);
	  }
	}
  ```
  4. Run As-->Run Configurations...-->选中wordcount-->在右边页面选择(x)=Arguments-->
  在Program arguments:中填入
  ```
  hdfs://localhost:9000/wlt/input hdfs://localhost:9000/wlt/output1
  ```
  一个输入文件地址，一个输出地址，中间空格隔开，输出地址不能存在
 -->Apply and Run
 
 5. 刷新查看结果
 
 ## 6.上传文件
 ```import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.URI;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IOUtils;

public class PutFile {

    public static void main(String[] args) throws IOException {
        //本地文件路径
        String local="/root/test.txt";
        String dest="hdfs://192.168.1.25:8020/user/root/wordcount/input/test2.txt";
        InputStream in=new BufferedInputStream(new FileInputStream(local));
        Configuration cfg=new Configuration();
        FileSystem fs=  FileSystem.get(URI.create(dest),cfg);
        OutputStream out=fs.create(new Path(dest));
        IOUtils.copyBytes(in, out,4096,true);
        fs.close();
        IOUtils.closeStream(in);
    }
}
```
## 7.下载文件
```
import java.io.IOException;
import java.net.URI;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;


public class Download {
	public static void main(String[] args) throws IOException{
		String hdfsPath="hdfs://localhost:9000/user/hadoop/input/yarn-site.xml";
		String localPath="/home/nolansheng";
		Configuration conf=new Configuration();
		FileSystem fs=FileSystem.get(URI.create(hdfsPath),conf);
		Path hdfs_path=new Path(hdfsPath);
		Path local_path=new Path(localPath);
		fs.copyToLocalFile(hdfs_path, local_path);
		fs.close();
		
	}
}
```

## 8. 读取文件
```
import java.io.IOException;
import java.io.InputStream;
import java.net.URI;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IOUtils;


public class Read {
	public static void main(String[] args) throws IOException{
		String uri="hdfs://localhost:9000/nohup.txt";
		Configuration cfg=new Configuration();
		FileSystem fs=FileSystem.get(URI.create(uri),cfg);
		InputStream in=null;
		try {
			in=fs.open(new Path(uri));
			IOUtils.copyBytes(in,System.out,4096,false);
		} catch (Exception e) {
			System.out.println(e.getMessage());
			
			// TODO: handle exception
		}finally {
			IOUtils.closeStream(in);
		}
		
	}

}
```

## 9.创建目录
```
import java.io.IOException;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;


public class Creatdir {
	public static void main(String[] args) throws IOException{
		String rootPath="hdfs://localhost:9000";
		Path p=new Path(rootPath+"/nolansheng/");
		Configuration conf=new Configuration();
		FileSystem fs=p.getFileSystem(conf);
		boolean b=fs.mkdirs(p);
		System.out.println(b);
		fs.close();
		
	}
}
```

## 10.删除文件
```
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

public class DeleteFile {
	public static void main(String[] args) {
		String uri="hdfs://localhost:9000/user/hadoop/input";
		Path path=new Path(uri);
		Configuration conf=new Configuration();
		try {
			FileSystem fs=path.getFileSystem(conf);
			boolean b1=fs.delete(path,true);
			fs.close();
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
		}
		
		
	}
}
```



# 更改权限
hdfs dfs -chmod 777 /(不然无法在网页或者eclipse直接删除等等）

# [将JAVA程序打包成jar文件直接运行](https://blog.csdn.net/yuzhuzhong/article/details/51654717)


# [HDFS Java API 参考](https://blog.csdn.net/chengyuqiang/article/details/60138407)

# eclipse下开发mapreduce需要导入的jar包
1. hadoop-2.7.2/share/hadoop/mapreduce下的所有jar包（子文件夹下的jar包不用）


2. hadoop-2.7.2/share/hadoop/common下的hadoop-common-2.7.2.jar

3. hadoop-2.7.2/share/hadoop/common/lib下的commons-cli-1.2.jar

