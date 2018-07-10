title: Ruby on Rails中nokogiri问题的解决方案

date: 2015-10-28 16:45:40

tags: 

- ruby
- debug

---
> 本文旨在解决rails server时报错的问题。

<!--more--> 
# 起因

最近打算摸索一下[Ruby on Rails](http://rubyonrails.org/), 然而一看官方教程运行

``` ruby
rails server
```

# 错误

出现错误如下：

``` 
Could not find gem 'byebug (>= 0) ruby' in any of the gem sources listed in your Gemfile or available on this machine.
Run `bundle install` to install missing gems.
```

然后根据提示运行了（注：此处翻墙安装同样会出现错误）

``` 
bundle install
```

之后又出现警告：

``` 
Installing nokogiri 1.6.6.2 with native extensions

Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
```

错误内容为：

``` 
An error occurred while installing nokogiri (1.6.6.2), and Bundler cannot
continue.
Make sure that `gem install nokogiri -v '1.6.6.2'` succeeds before bundling.
```

按照提示运行了

``` 
sudo gem install nokogiri -v '1.6.6.2'
```

之后扔出现ERROR：

``` 
ERROR:  Error installing nokogiri:
	invalid gem: package is corrupt, exception while verifying: undefined method `size' for nil:NilClass (NoMethodError) in /Users/mrllover/.rvm/rubies/ruby-2.1.5/lib/ruby/gems/2.1.0/cache/nokogiri-1.6.6.2.gem
```

# 解决方案

于是Google了一下，[stackoverflow](http://stackoverflow.com/)上可选的解决方案有：

[Nokogiri error when running bundle install](http://stackoverflow.com/questions/17204152/nokogiri-error-when-running-bundle-install)

[Error installing Nokogiri on bundle install but already installed](http://stackoverflow.com/questions/29020478/error-installing-nokogiri-on-bundle-install-but-already-installed)

[nokogiri will not install - ERROR: Failed to build gem native extension [duplicate]](http://stackoverflow.com/questions/16028028/nokogiri-will-not-install-error-failed-to-build-gem-native-extension)

但之前我遇到过类似问题，当时的解决方案是这样的，请参考[Installing Nokogiri](http://www.nokogiri.org/tutorials/installing_nokogiri.html)

本人机子为mac os,方法如下，输入：

``` 
gem uninstall nokogiri
```

如已安装了多个版本会出现如下选择框：

``` 
Select gem to uninstall:
 1. nokogiri-1.6.4.1
 2. nokogiri-1.6.5
 3. All versions
```

选择uninstall all versions.

然后输入：

``` 
xcode-select --install
```

会下载并安装x-code command line developer tools.

安装完毕后重新安装nokogiri:

``` 
gem install nokogiri
```

完成后运行

``` 
bundle install
```

此处须知，bundle install的时候需翻墙，别问我为什么，这年头什么都容易被墙，没翻墙会报错.

完成安装后运行:

``` 
rails server
```

大功告成，可以开始玩Ruby咯。

***
> 如果觉得本文对您有帮助，不妨扫一扫下面的二维码给点打赏呗😌

![](http://7xny9b.com1.z0.glb.clouddn.com/wechat.jpg)

