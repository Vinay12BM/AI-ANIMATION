import React from "react";
import { Button } from "@/components/ui/button";
import { Slider } from "@/components/ui/slider";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { Card, CardContent } from "@/components/ui/card";
import { cn } from "@/lib/utils";

interface MotionControlsProps {
  selectedEffect: string;
  onEffectChange: (effect: string) => void;
  intensity: number;
  onIntensityChange: (intensity: number) => void;
  speed: number;
  onSpeedChange: (speed: number) => void;
  className?: string;
}

const MotionControls = ({
  selectedEffect,
  onEffectChange,
  intensity,
  onIntensityChange,
  speed,
  onSpeedChange,
  className,
}: MotionControlsProps) => {
  const effects = [
    { id: "water", name: "Water Ripples", color: "bg-blue-500" },
    { id: "wind", name: "Wind Effect", color: "bg-emerald-500" },
    { id: "particles", name: "Particles", color: "bg-purple-500" },
    { id: "sway", name: "Gentle Sway", color: "bg-amber-500" },
    { id: "clouds", name: "Moving Clouds", color: "bg-slate-400" },
  ];

  return (
    <Card className={cn("w-full", className)}>
      <CardContent className="p-4">
        <Tabs defaultValue="effects" className="w-full">
          <TabsList className="grid grid-cols-3 mb-4">
            <TabsTrigger value="effects">Effects</TabsTrigger>
            <TabsTrigger value="parameters">Parameters</TabsTrigger>
            <TabsTrigger value="advanced">Advanced</TabsTrigger>
          </TabsList>
          
          <TabsContent value="effects" className="space-y-4">
            <div className="text-sm font-medium mb-2">Motion Effects</div>
            <div className="flex flex-wrap gap-2">
              {effects.map((effect) => (
                <Button
                  key={effect.id}
                  variant={selectedEffect === effect.id ? "default" : "outline"}
                  className={cn(
                    "effect-badge",
                    selectedEffect === effect.id && "ring-2 ring-primary ring-offset-2 ring-offset-background"
                  )}
                  onClick={() => onEffectChange(effect.id)}
                >
                  <span className={cn("w-2 h-2 rounded-full mr-2", effect.color)} />
                  {effect.name}
                </Button>
              ))}
            </div>
            
            <div className="text-sm font-medium mt-6 mb-2">Effect Description</div>
            <p className="text-sm text-muted-foreground">
              {selectedEffect === "water" && "Creates realistic water ripple animations. Great for lakes, oceans, or any water surface."}
              {selectedEffect === "wind" && "Simulates wind blowing through leaves, grass, hair or fabric."}
              {selectedEffect === "particles" && "Adds floating particles like dust, snow, or light effects."}
              {selectedEffect === "sway" && "Creates a gentle swaying motion, perfect for plants, trees, or hanging objects."}
              {selectedEffect === "clouds" && "Animates clouds or fog with smooth, drifting movement."}
            </p>
          </TabsContent>
          
          <TabsContent value="parameters" className="space-y-4">
            <div>
              <div className="flex justify-between items-center mb-2">
                <label className="text-sm font-medium">Intensity</label>
                <span className="text-xs text-muted-foreground">{intensity}%</span>
              </div>
              <Slider
                value={[intensity]}
                min={0}
                max={100}
                step={1}
                onValueChange={(value) => onIntensityChange(value[0])}
                className="my-4"
              />
            </div>
            
            <div>
              <div className="flex justify-between items-center mb-2">
                <label className="text-sm font-medium">Speed</label>
                <span className="text-xs text-muted-foreground">{speed}x</span>
              </div>
              <Slider
                value={[speed]}
                min={0.1}
                max={2}
                step={0.1}
                onValueChange={(value) => onSpeedChange(value[0])}
                className="my-4"
              />
            </div>
            
            <div className="pt-4">
              <Button variant="outline" size="sm" className="mr-2">
                Reset
              </Button>
              <Button size="sm">Apply</Button>
            </div>
          </TabsContent>
          
          <TabsContent value="advanced" className="space-y-4">
            <div className="text-sm text-muted-foreground">
              Advanced settings will be available in a future update.
            </div>
          </TabsContent>
        </Tabs>
      </CardContent>
    </Card>
  );
};

export default MotionControls;
