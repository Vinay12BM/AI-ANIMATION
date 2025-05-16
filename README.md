import React from "react";
import { ToggleGroup, ToggleGroupItem } from "@/components/ui/toggle-group";
import { Slider } from "@/components/ui/slider";
import { Tooltip, TooltipContent, TooltipTrigger } from "@/components/ui/tooltip";
import { cn } from "@/lib/utils";
import { Play, RotateCcw } from "lucide-react";

interface DrawingToolsProps {
  tool: string;
  onToolChange: (tool: string) => void;
  brushSize: number;
  onBrushSizeChange: (size: number) => void;
  onClear: () => void;
  onPreview: () => void;
  className?: string;
}

const DrawingTools = ({
  tool,
  onToolChange,
  brushSize,
  onBrushSizeChange,
  onClear,
  onPreview,
  className,
}: DrawingToolsProps) => {
  return (
    <div className={cn("flex flex-col space-y-4", className)}>
      <div className="flex justify-between items-center">
        <div className="text-sm font-medium">Tools</div>
        <div className="flex space-x-2">
          <Tooltip>
            <TooltipTrigger asChild>
              <button
                onClick={onClear}
                className="p-2 rounded-md hover:bg-secondary text-muted-foreground hover:text-foreground transition-colors"
              >
                <RotateCcw className="h-4 w-4" />
              </button>
            </TooltipTrigger>
            <TooltipContent>Clear Selection</TooltipContent>
          </Tooltip>
          
          <Tooltip>
            <TooltipTrigger asChild>
              <button
                onClick={onPreview}
                className="p-2 rounded-md hover:bg-secondary text-muted-foreground hover:text-foreground transition-colors"
              >
                <Play className="h-4 w-4" />
              </button>
            </TooltipTrigger>
            <TooltipContent>Preview Animation</TooltipContent>
          </Tooltip>
        </div>
      </div>
      
      <ToggleGroup
        type="single"
        value={tool}
        onValueChange={(value) => {
          if (value) onToolChange(value);
        }}
        className="flex justify-between border rounded-md p-1 bg-secondary/50"
      >
        <ToggleGroupItem
          value="select"
          aria-label="Select tool"
          className="flex-1 text-xs font-medium"
        >
          Select
        </ToggleGroupItem>
        <ToggleGroupItem
          value="brush"
          aria-label="Brush tool"
          className="flex-1 text-xs font-medium"
        >
          Brush
        </ToggleGroupItem>
        <ToggleGroupItem
          value="erase"
          aria-label="Erase tool"
          className="flex-1 text-xs font-medium"
        >
          Erase
        </ToggleGroupItem>
      </ToggleGroup>
      
      {tool !== "select" && (
        <div className="space-y-2">
          <div className="flex justify-between items-center">
            <label className="text-xs text-muted-foreground">Brush Size</label>
            <span className="text-xs text-muted-foreground">{brushSize}px</span>
          </div>
          <Slider
            value={[brushSize]}
            min={1}
            max={50}
            step={1}
            onValueChange={(value) => onBrushSizeChange(value[0])}
          />
        </div>
      )}
    </div>
  );
};

export default DrawingTools;
