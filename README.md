# motion-lens

Core Image wrapper for RubyMotion

## Usage

### setup

```ruby
image_view = UIImageView.new
lens       = Motion::Lens.new(ci_image)
```

### defining filters

```ruby
sepia_filter = Motion::Lens.filter('CISepiaTone', intensity: 0.8)
blur_filter  = Motion::Lens.filter('CIGaussianBlur', radius: 10.0)
```

### adding filters

```ruby
lens.add(sepia_filter)
lens.add(blur_filter)
```

or

```ruby
lens.add(sepia_filter).add(blur_filter)
```

### providing updates

Not sure about this API because so much depends upon how the implementation
turns out

Could assign a UIImageView to auto-update

```ruby
lens.target = image_view
```

Or assign the layer of a UIImageView to auto-update

```ruby
lens.target = image_view.layer
```

Could take a block to call when an update is available

```ruby
lens.on_update do |ci_image|
  context          = CIContext.contextWithOptions(nil)
  cgi_image        = context.createCGImage(ci_image, fromRect: ci_image.extent)
  image_view.image = UIImage.imageWithCGImage(cgi_image)
end
```

Could pass a UIImage instead of a CIImage (probably not a good default)

```ruby
lens.on_update do |image|
  image_view.image = image
end
```

### updating filters

```ruby
sepia_filter.update(intensity: 0.6)
blur_filter.update(radius: 5.0)
```

-------------------------------------------------------------------------------

### Resources

* [Core Image Filter Reference](1)
* [xissburg/XBImageFilters](2)
* [BradLarson/GPUImage](3)

[1]: (https://developer.apple.com/library/ios/documentation/graphicsimaging/reference/CoreImageFilterReference/Reference/reference.html)
[2]: (https://github.com/xissburg/XBImageFilters)
[3]: (https://github.com/BradLarson/GPUImage)
