BTOUCH=/Developer/MonoTouch/usr/bin/btouch
SMCS=/Developer/MonoTouch/usr/bin/smcs
MONOXBUILD=/Library/Frameworks/Mono.framework/Commands/xbuild
VERSION=1.5.0

all: GoogleMaps.dll

GoogleMaps-iOS-$(VERSION).zip:
	curl -O https://dl.google.com/geosdk/GoogleMaps-iOS-$(VERSION).zip > $@
	unzip $@

GoogleMaps: GoogleMaps-iOS-$(VERSION).zip
	cp GoogleMaps-iOS-$(VERSION)/GoogleMaps.framework/Versions/A/GoogleMaps GoogleMaps

libarclite.a:
	curl -L https://github.com/dalexsoto/MonoTouch-PSPDFKit-bindings/raw/master/AlexTouch.PSPDFKit/libarclite.a > libarclite.a
	curl -L https://github.com/dalexsoto/MonoTouch-PSPDFKit-bindings/raw/master/AlexTouch.PSPDFKit/libarclite.linkwith.cs > libarclite.linkwith.cs

Resources/GoogleMaps.bundle: GoogleMaps-iOS-$(VERSION).zip GoogleMaps
	mkdir Resources
	cp -R GoogleMaps-iOS-$(VERSION)/GoogleMaps.framework/Versions/A/Resources/* Resources/GoogleMaps.bundle

GoogleMaps.dll: Makefile GoogleMaps.linkwith.cs ApiDefinition.cs StructsAndEnums.cs GoogleMaps Resources/GoogleMaps.bundle libarclite.a
	$(MONOXBUILD) /p:Configuration=Release GoogleMaps.csproj
	cp bin/Release/GoogleMaps.dll GoogleMaps.dll

prepare: Resources/GoogleMaps.bundle libarclite.a

clean:
	-rm -rf list ios Resources/ GoogleMaps-iOS-$(VERSION)/ bin/ obj/ *.sln *.userprefs *.dll *.o *.zip *.mdb GoogleMaps libarclite.a libarclite.linkwith.cs
