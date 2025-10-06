# Laravel-12-use-intervention-image-


01.  1st install just run this only
     ------------------------------
    composer require intervention/image


02.  2nd add controller or components (livewire)
     --------------------------------------------
      use Intervention\Image\ImageManager;
      use Intervention\Image\Drivers\Gd\Driver;

      if ($this->thumbnail_image) {
            // $name = "product-" . time() . "." . $this->thumbnail_image->getClientOriginalExtension();
            $name = "product-" . time() . ".webp";

            $image = $manager->read($this->thumbnail_image->getRealPath()); // ✅ একই manager ব্যবহার
            $image->encodeByExtension('webp', 85);
            
            // $path = $this->thumbnail_image->storeAs('products', $name, 'public');
            $path = 'products/' . $name;
            Storage::disk('public')->put($path, (string) $image->encode());
            $validated['thumbnail_image'] = $path;

            if ($this->productId && $this->thumbnail_path && Storage::disk('public')->exists($this->thumbnail_path)) {
                Storage::disk('public')->delete($this->thumbnail_path);
            }
        } else {
            $validated['thumbnail_image'] = $this->thumbnail_path ?? null;
        }
